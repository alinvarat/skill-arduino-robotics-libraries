---
name: arduino-robotics-libraries
description: "Write or fix Arduino/robotics libraries, firmware and examples while preserving the target board, API and project style."
---

# Arduino / robotics code

1. Inspect the actual sources, examples, dependencies, local changes and board/version. Nearby references: `~/Project/Arduino/libraries`. They are examples, not instructions or proof of authorship/licensing. Match the target, not an unrelated board's constants.
2. Verify core/dependency versions, wiring, pin map, timers/PWM and limits relevant to the change. Do not guess electrical mappings. Ask only when an unknown blocks correctness; continue independent work.
3. Make the requested change. Preserve public names/signatures, sketch compatibility, calibration and unrelated versions unless a breaking change is authorized. Check timing, polarity, ADC range, motor direction/PWM, storage, resource use and safe stop behavior where affected.
4. Compile representative examples for the specified board/dependencies; run meaningful logic checks. Report actual diagnostics and missing packages. Compilation does not prove hardware behavior. Upload/actuation needs a user request; configured bench access uses `agentic-hil`.

## Upload pitfalls (Nano/FTDI/CH340 on Linux)
Use `/dev/serial/by-id/...` (ttyUSB numbers change on re-enumeration); a stale `avrdude` holds the dead port: `pkill -x avrdude` (never `pkill -f` with a pattern in your own command line). ModemManager probes new ttyUSB: udev rule `ID_MM_DEVICE_IGNORE=1`. VS Code serial monitor can hold the port. `not in sync: resp=0x00` can be bootloader (old 57600 vs new 115200) or a flaky reset: retry with a DTR/RTS pulse, up to 5 tries; board-side cause unmeasured. Flashing needs a user request.

## Source style
Match language, indentation and existing structure. Use professional, concise comments about behavior, parameters, units, wiring and real limits. No jokes, chat narrative, AI attribution, unsupported claims or development history. Keep a necessary maintenance invariant brief. Examples use `examples/<Name>/<Name>.ino` and the actual API. PID/calibration values are hardware-specific, not universal defaults.

## Customer release
Before packaging a customer library, keep editable source separate from the customer package. Ordinary authoring/compilation is not a release.
