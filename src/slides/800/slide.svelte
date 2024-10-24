<script lang="ts">
	import { Code, Action, Transition } from '@animotion/core'

	let code: ReturnType<typeof Code>
</script>

<Code
	bind:this={code}
	lang="nix"
	theme="catppuccin-mocha"
	code={`
        flake = {
          herculesCI.ciSystems = [ "aarch64-linux" ];
          effects =
            let
              pkgs = inputs.nixpkgs.legacyPackages.aarch64-linux;
              hci-effects = inputs.hercules-ci-effects.lib.withPkgs pkgs;
            in
            _: {
              wave-upload-firmware = hci-effects.mkEffect {
                __hci_effect_mounts = builtins.toJSON {
                  "/dev/ttyACM0" = "ttyACM0";
                  "/dev/ttyACM1" = "ttyACM1";
                  "/sys/bus/usb" = "sys-bus-usb";
                  "/dev/bus/usb" = "dev-bus-usb";
                };
                effectScript = ''
                  set -x
                  \${pkgs.lib.getExe inputs.self.packages.aarch64-linux.flash-firmwave}
                '';
              };
            };
        };
			`}
	options={{ duration: 1000, stagger: 0.3, containerStyle: false }}
/>
