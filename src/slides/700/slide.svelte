<script lang="ts">
	import { Code, Action } from '@animotion/core'

	let code: ReturnType<typeof Code>
</script>

<Code
	bind:this={code}
	lang="nix"
	theme="catppuccin-mocha"
	options={{ duration: 1000, stagger: 0.3, containerStyle: false }}
	code={`{ self, ... }: {
  perSystem = { pkgs, lib, ... }:
    let
      rustToolchain = pkgs.pkgsBuildHost.rust-bin.fromRustupToolchainFile ../rust-toolchain.toml;
      craneLib = (self.inputs.crane.mkLib pkgs).overrideToolchain rustToolchain;
      commonArgs = { /* nativeBuildInputs, buildInputs ... */ };
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
/>

<Action
	undo={() => {
		code.selectLines`*`
	}}
	actions={[() => code.selectLines`4`, () => code.selectLines`5`, () => code.selectLines`7-14`, () => code.selectLines`17-22`]}
/>
