<script lang="ts">
	import { Code, Action } from '@animotion/core'

	let code: ReturnType<typeof Code>
</script>

<Code
	bind:this={code}
	lang="nix"
	theme="catppuccin-mocha"
	code={`{
  self,
  ...
}:
{
  perSystem =
    { pkgs, lib, ... }:
    let
      rustToolchain = pkgs.pkgsBuildHost.rust-bin.fromRustupToolchainFile ../rust-toolchain.toml;
      craneLib = (self.inputs.crane.mkLib pkgs).overrideToolchain rustToolchain;

      commonArgs = {
        nativeBuildInputs = with pkgs; [
          pkg-config
        ];
        buildInputs =
          pkgs.lib.optionals pkgs.stdenv.isLinux (
            with pkgs;
            [
              alsaLib
              alsa-lib
            ]
          )
          ++ pkgs.lib.optionals pkgs.stdenv.isDarwin (
            with pkgs.darwin.apple_sdk.frameworks;
            [
              IOKit
              CoreAudio
              CoreMIDI
            ]
          );
        src = lib.cleanSourceWith { src = craneLib.path ../.; };
        doCheck = false;
      };
      sub = dir: {
        cargoLock = ../\${dir}/Cargo.lock;
        cargoToml = ../\${dir}/Cargo.toml;
        postUnpack = ''
          cd $sourceRoot/\${dir}
          sourceRoot="."
        '';
      };
    in
    {
      packages = rec {
        default = frontpanel-firmware;
        frontpanel-client = craneLib.buildPackage (commonArgs // (sub "frontpanel-client"));
        frontpanel-icd = craneLib.buildPackage (commonArgs // (sub "frontpanel-icd"));
        frontpanel-firmware = craneLib.buildPackage (commonArgs // (sub "frontpanel-firmware"));
      };
    };
}`}
	options={{ duration: 1000, stagger: 0.3, containerStyle: false }}
/>

<Action
	undo={() => {
		code.selectLines`*`
	}}
	actions={[() => code.selectLines`2`, () => code.selectLines`9`, () => code.selectLines`11-14`, () => code.selectLines`18`, () => code.selectLines`*`]}
/>
