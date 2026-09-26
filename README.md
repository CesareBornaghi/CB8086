# CB8086

**A free educational 8086 assembly playground and debugger, built entirely with HTML, CSS and JavaScript.**

CB8086 helps students and teachers explore assembly programming, CPU registers, flags, segmented memory and program execution directly in a web browser. Its interface is inspired by classic Borland DOS development tools, with a modern microprocessor logo and an integrated source-level debugger.

**CB8086 is freely downloadable and free to use for teaching, classroom activities, laboratory exercises and independent study.** No subscription, activation key or paid software is required to run the downloaded application.

## Download and run

### Single-file edition

1. Download `CB8086.html` to your computer. On GitHub, open the file and use **Download raw file** rather than saving the GitHub page.
2. Open it in a modern desktop browser.
3. Choose a built-in example or load your own `.asm` file.
4. Press **F2** to assemble, **F7** to step through the program, or **F9** to run it.

The single-file edition includes its styles, scripts and logo. It works offline without installation, a local server, a database or external frameworks.

### Source edition

If you download the full source repository, open `dist/index.html` and keep its companion JavaScript, CSS and SVG files in the same directory. No build step is required. The `dist/` directory can also be served by a static web host.

The current application interface and built-in help are in Italian. This README is in English.

## Features

- Load, edit and download `.asm` source files.
- **Save As** with a custom filename and automatic `.asm` extension.
- Source editor with line numbers, execution markers and breakpoints.
- Inspect and edit 16-bit registers and memory bytes while execution is paused.
- Inspect CPU flags and a segmented **1 MiB** memory space.
- DOS-style terminal with supported character and line input/output services.
- Adjustable execution speed, pause and reset.
- Source listing, symbol information and error messages with line numbers.
- Five built-in examples: DOS output, array summation, keyboard input, factorial and string copying.

## Integrated debugger

- **Step into, step over and step out** for examining procedures and calls.
- **Run to cursor** to stop at a selected source location.
- **Conditional breakpoints**, hit thresholds, one-shot breakpoints and enable/disable controls.
- **Watch expressions** for registers, flags, symbols and memory, with optional interruption when a value changes.
- **Memory write watchpoints** that stop after an instruction writes to a selected physical address range.
- **Call stack** and raw stack memory inspection.
- **Reverse stepping** to restore CPU state, memory, terminal output and input queues, including recorded manual edits and errors.
- **Execution history** with JSON trace export.

History retains up to 300 events within an estimated 4 MiB budget. Older events are discarded; an event exceeding the budget cannot be reversed. A `REP` string operation is treated as a single instruction step.

### Keyboard shortcuts

| Shortcut | Action |
| --- | --- |
| F1 | Open the built-in guide |
| F2 | Assemble the source |
| F4 | Run to cursor |
| F7 | Step into |
| F8 | Step over a call |
| Shift + F8 | Step out of the active call |
| F9 | Run / continue |
| Escape | Pause execution |
| Alt + Left Arrow | Reverse the last recorded event |
| Ctrl + S | Download using the current filename |
| Ctrl + Shift + S | Save As |

Some browsers or operating systems may intercept shortcuts. Equivalent on-screen buttons are available. On macOS, the save shortcuts also accept Command instead of Ctrl.

## Learning with CB8086

Use the included examples to observe how instructions change registers and flags, follow loops and conditional jumps, inspect array data, trace `CALL`/`RET` and stack operations, or experiment with supported DOS interrupt services.

For example, add a watch for `AX`, set a conditional breakpoint such as `CX == 1`, then run a loop and inspect its final iteration. Reverse stepping lets you revisit a recent instruction and compare the state before and after it.

## Compatibility and limitations

CB8086 is an **educational source-level interpreter**, not a complete binary emulator or a replacement for the original TASM/TLINK toolchain.

- It supports a subset of TASM/MASM-style syntax and 8086 instructions. Open **F1 → Guide** for the implemented directives, instructions and interrupt services.
- Instruction addresses are **virtual**: each source instruction advances IP by one position. Instructions are not encoded as machine-code bytes in CS memory.
- It does not generate or execute `.COM` or `.EXE` binaries.
- `.MODEL SMALL` and `.MODEL TINY` are accepted syntactically, but both use fixed educational segments: CS=`1000h`, DS=ES=`2000h`, SS=`3000h`.
- Macros, `INCLUDE`, linking, FAR calls/jumps, arbitrary segment layouts, custom interrupt handlers and 8087 instructions are not implemented.
- Hardware peripherals, instruction timing, prefetch, the DOS loader and self-modifying machine code are not simulated.
- Validation does not reproduce every constraint of the original assembler. Supported DOS/BIOS services are simplified.

CB8086 is an independent project. It does not include Borland software and is not affiliated with or endorsed by Borland or Intel.

## Local files and privacy

Source loading, execution and debugging take place in the browser. The application does not upload your assembly files to a server. When browser storage is available, it remembers the current source and filename locally.

Saving starts a browser download; the browser controls the destination folder and may rename duplicate filenames. Exported debug traces may contain source-related information, register values and terminal data from your session.

## Source layout and checks

| File | Purpose |
| --- | --- |
| `dist/index.html` | Interface and built-in guide |
| `dist/core.js` | Parser, expressions, symbols and CPU interpreter |
| `dist/debugger.js` | Breakpoints, watches, call tracking and reverse history |
| `dist/app.js` | UI behavior and built-in examples |
| `dist/style.css` | Interface styling and responsive layout |
| `dist/logo.svg` | CB8086 microprocessor logo |

For the full source edition, the included checks can be run with Node.js:

```sh
node tests/core.test.cjs
node tests/debugger.test.cjs
```

Node.js is only needed to run these development checks, not to use the application.

## License and free educational use

CB8086 is released under the **[MIT License](LICENSE)**.

You may download and use it free of charge for educational purposes, copy it for students, modify it for lessons and redistribute it with the required copyright and permission notices.

The MIT License also permits non-educational and commercial use. Educational use is the project's intended focus, **not a restriction imposed by the license**. Modified versions are not required to use the same license, and downstream distributors may charge for their copies or services.

The software is provided **“as is,” without warranty**, as stated in the license. See [LICENSE](LICENSE) for the complete terms and the [official MIT License text](https://opensource.org/license/mit) for reference.

Copyright (c) 2026 Cesare Bornaghi.
