# Slides for "Deterministic Firmware with Nix"

I had the pleasure of giving a talk at NixCon 2024.

> This talk explores the application of Nix's deterministic build principles to firmware development, with a special focus on integrating hardware-in-the-loop (HIL) testing into CI/CD pipelines. We'll discuss how Nix can enhance firmware reliability, security, and reproducibility by ensuring consistent builds across different environments.

More information on [nixcon.org](https://talks.nixcon.org/nixcon-2024/talk/KEJM9Y/).

You can watch the talk on [YouTube](https://www.youtube.com/watch?v=oAzkHpSWhaI&t=19438s).

## Setup

Install dependencies:

```sh
pnpm i
```

Run the development server at <http://localhost:5173/>:

```sh
pnpm run dev
```

Build and preview deploy:

```sh
pnpm run build && pnpm run preview
```
