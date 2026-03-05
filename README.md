# 👻 Snap Racer VR

![Version](https://img.shields.io/badge/version-1.0.0-blue.svg)
![License](https://img.shields.io/badge/license-MIT-green.svg)
![Three.js](https://img.shields.io/badge/Three.js-0.160.0-black.svg)

An immersive 3D endless racing game built for the **Snapchat Games Lensathon** challenge. Experience high-speed VR-style racing with stunning neon aesthetics and addictive gameplay.


> **Replace `yourusername` with your actual GitHub username**

---

## ✨ Features

### Gameplay
- 🏎️ **Immersive 3D Racing** - VR-style first-person perspective
- 🎯 **Progressive Difficulty** - Speed increases as you survive
- 🎮 **Dual Controls** - Keyboard for desktop, touch for mobile
- 🏆 **High Score System** - Persistent leaderboard tracking
- ⚡ **60fps Performance** - Smooth gameplay on all devices

### Visual Design
- 🎨 **Neon Aesthetic** - Vibrant Snapchat-inspired colors
- ✨ **Particle Effects** - Dynamic speed trails and visual polish
- 🌟 **Animated Starfield** - Immersive space background
- 💡 **Glowing Elements** - Emissive materials for cyberpunk feel
- 📱 **Responsive UI** - Polished interface on any screen size

### Technical
- 🚀 **Single File** - Entire game in one HTML file
- 📦 **Zero Dependencies** - No npm install required
- 🌐 **Works Offline** - Play anywhere, anytime
- 💾 **LocalStorage** - Saves your progress automatically
- 🎵 **Web Audio** - Procedural sound effects

---

## 🎯 How to Play

### Desktop Controls
- **Arrow Keys** ⬅️➡️ or **A/D** - Switch lanes
- **Goal** - Dodge obstacles and survive as long as possible!

### Mobile Controls  
- **Tap Left/Right** buttons to change lanes
- **Swipe** for alternative control

### Objective
- Navigate through obstacles by switching lanes
- Speed increases over time - how far can you go?
- Beat your high score and challenge your friends!

---

---

## 🛠️ Tech Stack

| Technology | Purpose |
|------------|---------|
| **Three.js** | 3D graphics rendering engine |
| **JavaScript** | Game logic and mechanics |
| **WebGL** | Hardware-accelerated 3D graphics |
| **HTML5 Canvas** | Rendering surface |
| **CSS3** | UI styling and animations |
| **Web Audio API** | Procedural sound effects |
| **LocalStorage** | Persistent game data |

---

## 🏆 Snapchat Lensathon Categories

This project qualifies for:

✅ **3D Games**
- Full 3D environment with Three.js
- Character controller and camera system
- 3D obstacles and dynamic assets

✅ **Longform Game**
- Persistent data storage (high scores)
- Statistical tracking and progression
- Designed for multiple play sessions

---

## 📊 Game Mechanics

### Core Systems
- **Lane-based movement** - 3 lanes with smooth transitions
- **Obstacle spawning** - Procedural generation with difficulty scaling
- **Speed curve** - Exponential acceleration from 0.05 to 0.3
- **Collision detection** - AABB-based hit detection
- **Score calculation** - Distance × speed multiplier

### Performance Optimizations
- Object pooling for obstacles
- Efficient geometry reuse
- Minimal draw calls
- LOD (Level of Detail) optimization
- Requestanimationframe-based game loop

---

## 🎨 Design Philosophy

**Snapchat-Inspired Aesthetic:**
- Vibrant neon color palette (Pink #FF006E, Purple #8338EC, Cyan #00F5FF)
- High-contrast dark backgrounds for accessibility
- Emissive glowing UI elements
- Youth-focused, energetic design language
- Mobile-first responsive approach

**Typography:**
- System fonts for universal compatibility
- Bold headers for impact
- Clear hierarchy for readability

---

## 📱 Browser Support

| Browser | Desktop | Mobile |
|---------|---------|--------|
| Chrome | ✅ | ✅ |
| Firefox | ✅ | ✅ |
| Safari | ✅ | ✅ |
| Edge | ✅ | ✅ |
| Opera | ✅ | ✅ |

**Requirements:**
- Modern browser with WebGL support
- JavaScript enabled
- Recommended: 60Hz+ display for optimal experience

---

## 🔧 Customization

Want to modify the game? Here's how:

### Change Colors
Find this section in the HTML `<style>` block:
```css
:root {
  --neon-pink: #FF006E;    /* Change me! */
  --neon-blue: #00F5FF;    /* Change me! */
  --neon-purple: #8338EC;  /* Change me! */
}
```

### Adjust Difficulty
Find this in the JavaScript section:
```javascript
this.speed = 0.05;        // Starting speed
this.maxSpeed = 0.3;      // Maximum speed
```

### Modify Game Rules
Look for these variables:
```javascript
this.currentLane = 1;     // Starting lane (0, 1, or 2)
if (Math.random() < 0.02) // Obstacle spawn rate
```

---

## 📸 Screenshots

> **Add screenshots of your game here!**

### Main Menu
*Vibrant neon welcome screen with Snapchat ghost*

### Gameplay
*Immersive 3D racing view with obstacles*

### Game Over
*Statistics screen with high score display*

---

## 🎬 Demo Video

> **Add your gameplay video here!**

Record a quick 60-90 second video showing:
1. Main menu
2. Gameplay demonstration  
3. Lane switching mechanics
4. Game over screen

Upload to YouTube and link it here!

---

## 🌟 Highlights

### What Makes This Special
- **Single file simplicity** - No build process or dependencies
- **Production-ready code** - Clean, commented, maintainable
- **Cross-platform** - Works seamlessly on desktop and mobile
- **Professional polish** - AAA game aesthetics and UX
- **Performance optimized** - Smooth 60fps on low-end devices

### Learning Outcomes
- Advanced Three.js 3D graphics
- Game loop architecture
- Collision detection algorithms  
- Mobile-first responsive design
- LocalStorage data persistence
- Web Audio API sound synthesis

---

## 🤝 Contributing

Contributions are welcome! Here are some ideas:

- 🎮 Add power-ups (shields, speed boosts)
- 🎵 Enhanced sound effects and music
- 🏆 Global leaderboard system
- 🎨 New vehicle skins
- 🌍 Different environment themes
- 👥 Multiplayer mode

**To contribute:**
1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Submit a pull request

---

## 📄 License

MIT License - feel free to use this project for:
- Learning and education
- Portfolio demonstrations
- Competition submissions
- Personal or commercial projects

See `LICENSE` file for full details.

---

## 🙏 Acknowledgments

- **Snapchat** - For hosting the Games Lensathon challenge
- **Three.js Team** - For the amazing 3D graphics library
- **WebGL Community** - For tutorials and documentation
- **Inspiration** - Endless runner games and VR racing experiences
---

## 🎯 Roadmap

### Completed ✅
- [x] Core 3D racing mechanics
- [x] Obstacle system
- [x] High score tracking
- [x] Mobile controls
- [x] Visual effects

### Planned 🚀
- [ ] Power-up system
- [ ] Multiple game modes
- [ ] Daily challenges
- [ ] Achievement system
- [ ] Sound toggle option
- [ ] Customizable vehicles
- [ ] Global leaderboard

---

## 🏁 Final Notes

This game was created as a submission to the **Snapchat Games Lensathon 2025**. The challenge was to build engaging games for Snapchat's platform, and this project showcases:

- Creative use of 3D web technologies
- Snapchat's vibrant brand aesthetic  
- Mobile-first game design
- Social gaming mechanics

**Thanks for playing! 👻🏎️**

---

<div align="center">


Made with ❤️ for the Snapchat Games Lensathon

⭐ Star this repo if you enjoyed the game!

</div>
