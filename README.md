# Kinetix 🎬

> **High-Performance Kinetic Animation & Dynamics Engine for Aerix**  
> Physical spring oscillators, Robert Penner easing equations, 2D particle systems, sub-millisecond native clocks, TrueColor terminal canvas rendering, and external FFmpeg GIF/video animation pipelines.

---

## 🌟 Overview

**Kinetix** is a high-precision animation and kinetic dynamics framework for Aerix. Designed to bridge the gap between static CLI apps and fluid visual experiences, Kinetix delivers physics-driven spring motion, complex particle explosions, keyframe timeline sequencing, and direct integration with external animation tools like **FFmpeg** to produce animated GIFs, MP4 videos, and interactive terminal animations.

---

## 📁 Organized Package Structure

```
Kinetix/
├── aerix.json              # Package manifest (v1.1.0)
├── README.md               # Documentation & guides
├── LICENSE                 # MIT License
├── examples/
│   └── demo.arx            # Verification & showcase suite
└── src/
    ├── mod.arx             # Master module export
    ├── core/
    │   ├── clock.arx       # Win32 sub-millisecond clock & frame regulator (FFI)
    │   └── timeline.arx    # Keyframe animation timeline & tracks
    ├── math/
    │   ├── easing.arx      # Robert Penner easing curves (Quad, Cubic, Bounce, Back)
    │   └── vector.arx      # 2D kinematic vectors (Vec2, distance, lerp, normalize)
    ├── physics/
    │   ├── spring.arx      # 1D & 2D damped harmonic springs (Hooke's Law)
    │   └── particles.arx   # Kinetic particle emitters & explosion bursts
    ├── graphics/
    │   ├── canvas.arx      # 24-bit TrueColor canvas with PPM frame export
    │   ├── fx.arx          # Kinetic text effects (typewriter, wave, shimmer, glitch)
    │   └── player.arx      # Flicker-free ANSI terminal animation player
    └── exporters/
        ├── ffmpeg.arx      # FFmpeg-driven animated GIF & MP4 video generator
        ├── svg.arx         # Vector SMIL & CSS keyframe animated SVG exporter
        └── tools.arx       # System CLI probing & process pipeline runner
```

---

## ✨ Features

- ⏱️ **Sub-Millisecond Native Clock (`KinetixClock`)**: Win32 `kernel32.dll` tick-precision frame timing, delta-time calculations, and exact FPS throttling (30, 60, 120 FPS).
- 🎬 **Keyframe Timelines (`Timeline`, `AnimationTrack`)**: Multi-track property animations with dynamic curve easing.
- 📈 **Mathematical Easing Curves (`Kinetix.Easing`)**: Complete suite of Robert Penner easing functions (`ease_in_quad`, `ease_out_quad`, `ease_in_out_cubic`, `ease_out_bounce`, `ease_by_name`).
- 🪓 **Harmonic Damped Springs (`Spring`, `Spring2D`)**: Real-time Hooke's Law simulation with configurable stiffness, damping, mass, and 2D target tracking.
- 🎆 **2D Particle Burst Emitters (`ParticleEmitter`)**: Velocity-based kinematic particles with gravity, lifespan decay, and TrueColor RGB styling.
- 🎨 **Double-Buffered TrueColor Virtual Canvas (`Canvas`)**: 24-bit ANSI terminal canvas with `draw_rect`, `draw_circle`, `draw_line`, `draw_text`, and PPM image exporting.
- 🎥 **FFmpeg Animated GIF & Video Renderer (`FFmpegAnimationRenderer`)**: Automatically turns canvas frame sequences into smooth animated `.gif` and `.mp4` video files.
- 🌐 **Animated Vector SVG Exporter (`SvgAnimator`)**: Generates hardware-accelerated animated SVGs playable directly in any browser.

---

## 🚀 Installation

Install via the official Aerix Package Manager:

```bash
arx pkg install Kinetix
```

Aerix automatically installs `Kinetix` directly into your global Aerix installation modules directory (`C:\Aerix\modules\Kinetix`).

---

## 📖 Code Examples

### 1. Generating an Animated GIF with FFmpeg

```aerix
import Kinetix

fn main() -> void {
    let frames = List<Canvas>()
    
    // Generate 30 frames of animation
    mut i = 0
    while i < 30 {
        let canvas = Canvas(40, 12)
        canvas.draw_rect(0, 0, 40, 12, "#", 0, 150, 255)
        
        let t = (i as f64) / 30.0
        let ball_y = 2 + ((ease_out_bounce(t) * 7.0) as i64)
        canvas.draw_circle(20, ball_y, 1, "O", 255, 200, 50)
        
        frames.push(canvas)
        i = i + 1
    }

    // Automatically writes frames, invokes FFmpeg, and cleans up temp files
    FFmpegAnimationRenderer.render_frames_to_gif(frames, "bouncing_ball.gif", 30)
}
```

### 2. Spring Physics Motion (2D)

```aerix
import Kinetix

fn main() -> void {
    // Initial (0,0), Target (80, 40), Stiffness 100.0, Damping 12.0
    let spring = Spring2D(0.0, 0.0, 80.0, 40.0, 100.0, 12.0)

    while !spring.is_settled(0.5) {
        spring.update(0.016) // 60 FPS delta
        println("Pos: (" + (spring.get_x() as str) + ", " + (spring.get_y() as str) + ")")
    }
}
```

### 3. Keyframe Animation Timeline

```aerix
import Kinetix

fn main() -> void {
    let track = AnimationTrack("scale")
    track.add_keyframe(0.0, 0.0, "linear")
    track.add_keyframe(1.0, 100.0, "bounce_out")
    track.add_keyframe(2.0, 50.0, "cubic_in_out")

    let val_at_half = track.evaluate(0.5)
    println("Value at 0.5s: " + (val_at_half as str))
}
```

---

## 📄 License

MIT © HaxOrWot
