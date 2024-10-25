<script lang="ts">
	import { Code } from '@animotion/core'

	let code: ReturnType<typeof Code>
</script>

<div class="flex h-screen w-screen items-center justify-center border-none bg-[#1e1e2e]">
	<Code
		bind:this={code}
		lang="nix"
		theme="catppuccin-mocha"
		options={{ duration: 1000, stagger: 0.3, containerStyle: false }}
		code={`{ clangStdenv
, runCommand
, xorg
, gcc-arm-embedded
, python3
, nrfutil
, cmake
, gtest
, fetchFromGitHub
, fetchzip
, microsoft-gsl
, juce
, freetype
, pkg-config
, curl
, ut
, fmt
, eigen-genki
, etl
, boost-sml
, range-v3
, alsa-lib
,
}:
let
  nrf52-sdk-src = fetchzip {
    url = "https://nsscprodmedia.blob.core.windows.net/prod/software-and-other-downloads/sdks/nrf5/binaries/nrf5sdk15209412b96.zip";
    hash = "sha256-5OyGd9feYw5puG4OpraJtdmbqm4F4TJ0tXzXFbwRNac=";
  };

  nrf52-sdk = runCommand "" { } ''
    cp -r \${nrf52-sdk-src} ./source
    chmod -R +w source
    cd source
    cp -r \${micro-ecc} external/micro-ecc/micro-ecc
    rm -rf components/toolchain/cmsis
    cd -
    cp -r source $out
  '';

  micro-ecc = fetchFromGitHub {
    repo = "micro-ecc";
    owner = "kmackay";
    rev = "601bd11062c551b108adbb43ba99f199b840777c";
    hash = "sha256-QTS0P2EkB1pApVUStjcKPNjHeS5Ets3Bh4j3g22CIDk=";
  };
  cmsis-dsp = fetchFromGitHub {
    repo = "CMSIS-DSP";
    owner = "ARM-software";
    rev = "v1.11.0";
    hash = "sha256-9i96wfpAqwohyWzE60tHaOMoGDohw1goEI9zdPGDJoY=";
  };
  cmsis-5 = fetchFromGitHub {
    repo = "CMSIS_5";
    owner = "ARM-software";
    rev = "5.9.0";
    hash = "sha256-m3V5pu/ao1d7aVhlWh0lvesAXmYA5JpOVsumAi1Wioc=";
  };
in
clangStdenv.mkDerivation {
  name = "firmwave";

  src = ../.;

  buildInputs = [
    xorg.libX11
    xorg.libX11.dev
    xorg.libXext
    xorg.libXinerama
    xorg.libXrandr
    xorg.libXcursor
    xorg.libXdmcp
    xorg.libXtst
    freetype
    alsa-lib
    microsoft-gsl
    juce
    curl
    gtest
    ut
    fmt
    etl
    boost-sml
    eigen-genki
    range-v3
  ];

  prePatch = ''
    cd firmwave
    substituteInPlace tests/CMakeLists.txt --replace-fail "gtest_main" " \${gtest}/lib/libgtest.so \${gtest}/lib/libgtest_main.so "
    substituteInPlace ../common/tests/CMakeLists.txt --replace-fail "gtest_main" " \${gtest}/lib/libgtest.so \${gtest}/lib/libgtest_main.so "
  '';

  preConfigure = ''
    cp -r --no-preserve=mode \${nrf52-sdk} $TMP/nrf52-sdk
    export cmakeFlagsArray+=("-DCMAKE_CXX_FLAGS=-I\${ut}/include/ut-2.0.1/include -I\${cmsis-5}/CMSIS/Core/Include -I\${boost-sml}/include")
    export cmakeFlagsArray+=("-DCMAKE_C_FLAGS=-I\${ut}/include/ut-2.0.1/include -I\${cmsis-5}/CMSIS/Core/Include -I\${boost-sml}/include")
  '';

  installPhase = ''
    mkdir $out
    for i in $(find . -name '*.hex' -o -name '*.zip')
    do
      mv "$i" "$out"
    done
  '';

  cmakeFlags = [
    #    "--trace-expand"
    "-DCMAKE_BUILD_TYPE=Release"
    "-DCMAKE_TOOLCHAIN_FILE=\${./toolchain.cmake}"
    "-DCPM_nrf52-sdk_SOURCE=/build/nrf52-sdk"
    "-DCPM_CMSISDSP_SOURCE=\${cmsis-dsp}"
    "-DCPM_CMSIS_SOURCE=\${cmsis-5}"
    "-DFETCHCONTENT_FULLY_DISCONNECTED=ON"
    "-DCPM_USE_LOCAL_PACKAGES=ON"
  ];

  installCheckPhase = ''
    ctest --test-dir .
  '';

  doInstallCheck = true;

  nativeBuildInputs = [
    python3.pkgs.intelhex
    nrfutil

    gcc-arm-embedded
    cmake
    pkg-config
  ];
}`}
	/>
</div>

<style>
	* {
		font-size: 10.5px;
		background-color: #1e1e2e;
	}
	div {
		background-color: #1e1e2e !important;
	}
</style>
