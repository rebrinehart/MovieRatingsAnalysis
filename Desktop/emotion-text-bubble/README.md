# 🍎 Text Reponsive Emotion Sticker - iOS iMessage Extension

iOS iMessage extension that automatically detects emotions bsaed on the text and creates a colored text bubbles based on the emotional content. Model is trained on the GoEmotion dataset consisting of 28 emotions.

## Video Demo

Watch the emotion-responsive text bubble extension in action:

https://github.com/user-attachments/assets/demo.mp4

**📹 Features Demonstrated:**
- Real-time emotion detection as you type
- Dynamic bubble color changes based on detected emotions
- Sticker creation and sharing in iMessage
- Smooth UI interactions and emotion preview

> **Video Shows**: Complete workflow from typing emotional text to creating and sharing colored bubble stickers in the iOS Messages app.

## ✨ Features

- **Real-time Emotion Detection**: Analyze text emotions as you type
- **28 Emotion Categories**: Comprehensive emotion recognition based on GoEmotion
- **Sticker Creation**: Convert emotional text into shareable iMessage stickers
- **85.4% Accuracy**: Emotion classification model using CoreML
- **CoreML Optimization**: 1.2 MB model optimized for iOS
- **GoEmotion Dataset**: Trained on 58,009 text samples with labled emotion
- **Messages Extension**: Seamless integration with iOS Messages app

## 🚀 Quick Start

### Installation
1. **Clone the repository**
   ```bash
   git clone [repository-url]
   cd emotion-text-bubble
   ```

2. **Open in Xcode**
   ```bash
   open emotion-text-bubble.xcodeproj
   ```

3. **Build and Run**
   - Select target device/simulator
   - Press ⌘R to build and run

### Testing the Messages Extension
1. Open Messages app in simulator
3. Tap the + icon bottom left of the message area
4. Scroll and select emotion-text-bubble app
5. Type your text in the input box to preview

## 🏗️ Project Architecture

### Core Components

```
emotion-text-bubble/
├── 📱 Main App
│   ├── AppDelegate.swift
│   ├── ViewController.swift
│   └── Main.storyboard
├── 💬 Messages Extension
│   ├── MessagesViewController.swift
│   ├── MainInterface.storyboard
│   └── Info.plist
└── 🔄 Shared Components
    ├── EmotionDetector.swift      # CoreML integration
    ├── EmotionColors.swift        # Emotion-color mapping
    ├── BubbleRenderer.swift       # Custom bubble graphics
    ├── EmotionClassifier.mlmodel  # Trained ML model
    └── emotion_color_mapping.json # Color configuration
```

### Classes

#### `EmotionDetector.swift`
- **Purpose**: CoreML model wrapper for emotion classification
- **Features**: Text preprocessing, model loading, prediction handling
- **Input**: Raw text string
- **Output**: Single emotion label (e.g., "joy", "anger", "excitement")

#### `EmotionColors.swift`
- **Purpose**: Maps emotions to appropriate colors
- **Features**: 28 emotion-color mappings, JSON configuration loading
- **Psychology**: Colors chosen based on GoEmotions mapping
- **Format**: Returns UIColor objects for iOS rendering

#### `BubbleRenderer.swift`
- **Purpose**: Creates iMessage-style text bubbles
- **Features**: Core Graphics rendering, gradients, shadows, proper geometry
- **Customization**: Emotion-based coloring, typography, bubble tails
- **Output**: UIImage suitable for sticker creation

#### `MessagesViewController.swift`
- **Purpose**: Main Messages extension interface
- **Features**: Real-time text analysis, sticker creation
- **User Flow**: Type text → See emotion → Preview bubble sticker → Share sticker

## 🔬 Data Analysis and Model Training

### Dataset Analysis
1. **GoEmotion Dataset**: 58,009 unique text samples with 28 possible emotion annotations curated comments extracted from Reddit. Total of 211k+ data as multiple raters may have rated the same comment
2. **Multilabel Strategy**: Preserve all human rater judgments (min_votes=1)
3. **Format Conversion**: One-hot encoding → comma-separated labels to allow multiple emotions per data

### Model Training
1. **Framework**: CreateML's MLTextClassifier
2. **Approach**: Direct multilabel training for optimal performance
3. **Optimization**: Automatic multilabel→single-label conversion by MLTextClassifier
Most model training details are handled by CreateML framework and MLTextClassifier

### Results
- **Accuracy**: 85.4% in predicting text emotion
   - **Note**: If a text had multiple emotions from raters (ex. ['joy', 'excitement']) and the model predicts any one of those (either joy or excitement), it will be classified as correct. 
- **Model Ability**: 28-class emotion classification
- **Deployment**: Production-ready CoreML .mlmodel

## Reflection

### Potential Improvements
- **Multi-language Support**: Extend beyond English text
- **Emotion Intensity**: Detect emotional strength levels
- **Custom Colors**: User-configurable emotion color themes
- **Animation**: Animated bubble transitions and effects
- **Voice Messages**: Emotion detection from speech-to-text

### Technical Upgrades
- **Model Accuracy**: Explore transformer models for better performance
- **Real-time Training**: Personalized emotion detection adaptation
- **Cloud Integration**: Sync emotion preferences across devices
- **Advanced Rendering**: 3D bubble effects and particle systems