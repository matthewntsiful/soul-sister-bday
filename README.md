# Soul Sister Birthday Website

<div align="center">
  <img src="https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white" alt="HTML5" />
  <img src="https://img.shields.io/badge/CSS3-1572B6?style=for-the-badge&logo=css3&logoColor=white" alt="CSS3" />
  <img src="https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black" alt="JavaScript" />
  <img src="https://img.shields.io/badge/Nginx-009639?style=for-the-badge&logo=nginx&logoColor=white" alt="Nginx" />
  <img src="https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white" alt="Docker" />
</div>

A beautiful, containerized birthday celebration website for a special soul sister, featuring a responsive design, photo gallery, personalized message, and background music.

## Live Demo

<div align="center">
  <h3>🎉 This project is hosted on GitHub Pages 🎉</h3>
  <h2><a href="https://matthewntsiful.github.io/soul-sister-bday/" target="_blank">https://matthewntsiful.github.io/soul-sister-bday/</a></h2>
  <p>Visit the link above to see the live birthday celebration website!</p>
</div>

## Table of Contents

1. [Overview](#overview)
2. [Architecture](#architecture)
3. [Installation](#installation)
4. [Configuration](#configuration)
5. [Usage](#usage)
6. [Project Structure](#project-structure)
7. [Customization](#customization)
8. [Troubleshooting](#troubleshooting)

## Overview

The Soul Sister Birthday Website is a containerized static website built to celebrate a special person's birthday. The site is served using Nginx within a Docker container, making it easy to deploy anywhere Docker is available.

**Key Features:**
- Responsive design that adapts beautifully to any screen size
- Interactive photo gallery using Lightbox for an enhanced viewing experience
- Background music with toggle functionality
- Personalized birthday message/poem
- Docker containerization for easy deployment and consistent environment

## Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                        Docker Host                          │
│                                                             │
│   ┌─────────────────────────────────────────────────────┐   │
│   │                Docker Container                     │   │
│   │                                                     │   │
│   │   ┌─────────────┐          ┌───────────────────┐    │   │
│   │   │             │          │                   │    │   │
│   │   │  Nginx      │ serves   │  Static Website   │    │   │
│   │   │  Web Server │◄────────►│  - HTML           │    │   │
│   │   │  (Port 8080)│          │  - CSS            │    │   │
│   │   │             │          │  - JavaScript     │    │   │
│   │   └─────────────┘          │  - Images         │    │   │
│   │          │                 │  - Audio          │    │   │
│   │          │                 └───────────────────┘    │   │
│   │          │                                          │   │
│   │          │ configured by                            │   │
│   │          ▼                                          │   │
│   │   ┌─────────────┐                                   │   │
│   │   │ nginx.conf  │                                   │   │
│   │   └─────────────┘                                   │   │
│   │                                                     │   │
│   └─────────────────────────────────────────────────────┘   │
│                                                             │
│                          │                                  │
│                          │ exposed via                      │
│                          ▼                                  │
│                    ┌──────────┐                             │
│                    │ Port 8080│                             │
│                    └──────────┘                             │
│                          │                                  │
└─────────────────────────────────────────────────────────────┘
                           │
                           │ accessed by
                           ▼
                    ┌──────────────┐
                    │   Browser    │
                    └──────────────┘
```

### Components

1. **Static Website Files**
   - HTML, CSS, and JavaScript files
   - Image assets and audio files
   - Provides the user interface and functionality

2. **Nginx Web Server**
   - Serves the static website files
   - Handles HTTP requests
   - Provides caching and compression

3. **Docker Container**
   - Encapsulates the web server and website files
   - Provides consistent environment
   - Enables easy deployment

## Installation

### Prerequisites

- Docker and Docker Compose
- Git

### Setup

1. Clone the repository:
   ```bash
   git clone <repository-url>
   cd soul-sister-bday
   ```

2. Start the application:
   ```bash
   docker-compose up -d
   ```

3. Access the website:
   - Birthday website: http://localhost:8080

## Configuration

### Nginx Configuration

The web server is configured in the `nginx.conf` file:

```nginx
server {
    listen 8080;
    server_name localhost;

    # Root directory for website files
    root /usr/share/nginx/html;
    index index.html;

    # Cache settings for static assets
    location ~* \.(jpg|jpeg|png|gif|ico|css|js|mp3)$ {
        expires 30d;
        add_header Cache-Control "public, no-transform";
    }

    # Enable gzip compression
    gzip on;
    gzip_types text/plain text/css application/javascript application/json;
}
```

### Docker Configuration

The application uses Docker Compose for container orchestration:

```yaml
version: '3.8'

services:
  web:
    build: .
    ports:
      - "8080:8080"
    volumes:
      - ./assets:/usr/share/nginx/html/assets
      - ./index.html:/usr/share/nginx/html/index.html
      - ./style.css:/usr/share/nginx/html/style.css
    restart: always
```

## Usage

### Viewing the Birthday Website

1. Access the website at http://localhost:8080
2. View the main hero section with the birthday greeting
3. Click the "Open Your Special Message" button to scroll to the personalized message
4. Browse through the photo gallery (click on images to view them in a lightbox)
5. Toggle the background music using the music button in the bottom-right corner

## Project Structure

```
soul-sister-bday/
├── assets/
│   ├── gallery/
│   │   ├── 1.jpg
│   │   ├── 2.jpg
│   │   ├── 3.jpg
│   │   ├── 4.jpg
│   │   └── 5.jpg
│   ├── music/
│   │   └── birthday-song.mp3
│   └── sister-image.jpg
├── docker-compose.yml
├── Dockerfile
├── index.html
├── nginx.conf
├── README.md
└── style.css
```

## Customization

To customize the website for your own use:

1. **Images**: Replace the images in the `assets/gallery/` directory and update `sister-image.jpg`
2. **Music**: Replace `assets/music/birthday-song.mp3` with your preferred audio
3. **Message**: Edit the message content in `index.html` within the `poem-section`
4. **Styling**: Modify colors, fonts, and other visual elements in `style.css`
5. **Name**: Update the signature and any name references in the HTML

### Personalized Message

The personalized birthday message can be customized in the `index.html` file:

```html
<div class="poem-text">
    <p>To the one who knows my heart without me speaking a word,</p>
    <p>Who has held my hand through storms and sunshine alike,</p>
    <!-- Additional message content -->
</div>
```

## Troubleshooting

### Common Issues

1. **Website not loading**
   - Check Docker container status: `docker-compose ps`
   - Verify Nginx logs: `docker-compose logs web`
   - Ensure port 8080 is available on your system

2. **Images not displaying**
   - Check file paths in the HTML
   - Verify image files exist in the correct directories
   - Check browser console for 404 errors

3. **Music not playing**
   - Check if the audio file exists at `assets/music/birthday-song.mp3`
   - Verify browser permissions for autoplay
   - Check browser console for media-related errors

## Powered By

Made with ❤️ for a special soul sister