# Kinetix 🎬

> **High-Performance Kinetic Animation & Dynamics Engine for Aerix**  
> Physical spring oscillators, Robert Penner easing equations, 2D particle systems, sub-millisecond native clocks, TrueColor terminal canvas rendering, and external pipeline tool integration.

---

## 🌟 Overview

**Kinetix** is a zero-dependency, high-precision animation and kinetic dynamics framework written in 100% pure native Aerix. Designed to bridge the gap between static CLI apps and fluid interactive visual experiences, Kinetix delivers physics-driven spring motion, complex particle explosions, frame-rate regulation, and seamless integration with external CLI rendering tools like `ffmpeg`, `git`, and system processes.

---

## ✨ Features

- ⏱️ **Sub-Millisecond Native Clock (`KinetixClock`)**: Win32 `kernel32.dll` tick-precision frame timing, delta-time calculations, and exact FPS throttling (30, 60, 120 FPS).
- 📈 **Mathematical Easing Curves (`Kinetix.Easing`)**: Complete suite of Robert Penner easing functions (`ease_in_quad`, `ease_out_quad`, `ease_in_out_cubic`, `ease_out_bounce`, `ease_out_elastic`).
- 🪓 **Harmonic Damped Spring Physics (`Spring`)**: Real-time Hooke's Law simulation with configurable stiffness, damping, mass, and velocity settling checks.
- 🎆 **2D Particle Burst Emitters (`ParticleEmitter`)**: Velocity-based kinematic particles with gravity, lifespan decay, TrueColor RGB styling, and bounding-box rendering.
- 🎨 **Double-Buffered TrueColor Virtual Canvas (`Canvas`)**: 24-bit ANSI terminal canvas with `draw_rect`, `draw_text`, `set_pixel`, and single-pass ANSI frame flushing.
- 🔤 **Kinetic Text FX (`Kinetix.Fx`)**: Dynamic typewriter effect, metallic shimmer gradients, and sinusoidal wave text animations.
- 🛠️ **External Tool Integration (`Kinetix.Tools`)**: Probing installed host tools (`git`, `curl`, `ffmpeg`, `powershell`), executing command-line rendering pipelines, and exporting animation frames.

---

## 🚀 Installation

Install via the official Aerix Package Manager:

```bash
arx pkg install Kinetix
```

Aerix automatically installs `Kinetix` directly into your global Aerix installation modules directory (`C:\Aerix\modules\Kinetix`), making it accessible from any project across your system!

---

## 📖 Quick Start

### 1. Spring Physics Motion

```aerix
import Kinetix

fn main() -> void {
    // Initial position: 0.0, Target: 100.0, Stiffness: 120.0, Damping: 14.0, Mass: 1.0
    let spring = Spring(0.0, 100.0, 120.0, 14.0, 1.0)

    while !spring.is_settled(0.5) {
        spring.update(0.016) // 60 FPS delta time
        println("Current Pos: " + (spring.position as str))
    }
    println("Spring settled at: " + (spring.position as str))
}
```

### 2. Particle Explosions

```aerix
import Kinetix

fn main() -> void {
    // Origin (x: 40.0, y: 15.0), Gravity: 9.8
    let emitter = ParticleEmitter(40.0, 15.0, 9.8)
    emitter.explode(16, 20.0, "✦")

    emitter.update(0.033)
    println("Active particles: " + (emitter.count_alive() as str))
}
```

### 3. High-Precision Frame Throttling

```aerix
import Kinetix

fn main() -> void {
    let clock = KinetixClock(60) // Target 60 FPS

    mut frame = 0
    while frame < 60 {
        let dt = clock.tick()
        // Render frame logic here...
        clock.sleep_frame()
        frame = frame + 1
    }
}
```

### 4. External Tool Pipeline & FFmpeg Video Export

```aerix
import Kinetix

fn main() -> void {
    if is_external_tool_available("ffmpeg") {
        println("FFmpeg is available on this system!")
        // Export frames to directory and compile video
        // render_video_with_ffmpeg("frames_out", "animation.mp4", 60)
    }
}
```

---

## 📄 License

MIT © HaxOrWot
