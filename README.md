# Static Website Hosting Using Docker

![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white)
![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=for-the-badge&logo=css3&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)
![Nginx](https://img.shields.io/badge/Nginx-009639?style=for-the-badge&logo=nginx&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![GitHub Pages](https://img.shields.io/badge/GitHub_Pages-222222?style=for-the-badge&logo=github&logoColor=white)

A containerized static website implementation showcasing modern web development and DevOps practices. Features responsive design, interactive elements, media integration, and optimized Nginx configuration for production deployment.

## Live Demo

🎉 **This project is hosted on GitHub Pages** 🎉

**[https://matthewntsiful.github.io/soul-sister-bday/](https://matthewntsiful.github.io/soul-sister-bday/)**

Visit the link above to see the live birthday celebration website!

## Table of Contents

1. [Overview](#overview)
2. [Architecture](#architecture)
3. [Installation](#installation)
4. [Configuration](#configuration)
5. [Usage](#usage)
6. [Project Structure](#project-structure)
7. [Customization and Extension](#customization-and-extension)
8. [Troubleshooting](#troubleshooting)

## Overview

This project demonstrates a modern approach to static website hosting using Docker and Nginx. It implements industry best practices for containerization, web server configuration, and front-end development to create a production-ready web application that can be deployed anywhere Docker is available.

**Key Features:**

- Containerized deployment using Docker for consistent environments across development and production
- Optimized Nginx configuration with proper caching, compression, and security settings
- Responsive design implementation using modern CSS techniques
- Interactive elements with JavaScript for enhanced user experience
- Media optimization and delivery best practices
- GitHub Pages integration for cloud hosting
- Volume mounting for easy content updates without rebuilding containers

## Architecture

```text
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
   - Birthday website: [http://localhost:8080](http://localhost:8080)

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

1. Access the website at [http://localhost:8080](http://localhost:8080)
2. View the main hero section with the birthday greeting
3. Click the "Open Your Special Message" button to scroll to the personalized message
4. Browse through the photo gallery (click on images to view them in a lightbox)
5. Toggle the background music using the music button in the bottom-right corner

## Project Structure

```text
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

## Customization and Extension

This project is designed to be easily customizable and extensible:

1. **Content Management**: Update content by modifying files in the mounted volumes without rebuilding the container
2. **Performance Optimization**: Adjust Nginx caching and compression settings in `nginx.conf` for different deployment scenarios
3. **CI/CD Integration**: Easily integrate with CI/CD pipelines for automated testing and deployment
4. **Media Assets**: Optimize and replace media assets in the `assets/` directory following web performance best practices
5. **Styling**: Modify the CSS architecture in `style.css` to implement different design systems

### Code Structure

The HTML structure follows component-based organization for maintainability:

```html
<section class="component-section">
    <div class="component-container">
        <!-- Component content structure -->
        <h2 class="component-title">Title</h2>
        <div class="component-content">
            <!-- Content elements -->
        </div>
    </div>
</section>
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

Blakk Brother Inc
