# Juara Rakyat - Malaysian Anti-Scam Intelligence Platform

[![GitLab Pipeline](https://gitlab.com/Behelit-Systems/the-juara-rakyat/badges/main/pipeline.svg)](https://gitlab.com/Behelit-Systems/the-juara-rakyat/-/pipelines)
[![License: AGPL v3](https://img.shields.io/badge/License-AGPL_v3-blue.svg)](https://www.gnu.org/licenses/agpl-3.0)
[![Coverage](https://gitlab.com/Behelit-Systems/the-juara-rakyat/badges/main/coverage.svg)](https://gitlab.com/Behelit-Systems/the-juara-rakyat/-/commits/main)

## 🛡️ Overview

Juara Rakyat is an open-source anti-scam intelligence platform designed to protect Malaysian communities from digital fraud on WhatsApp and other messaging platforms. Using advanced detection algorithms, real-time analysis, and community-driven intelligence, we help identify, track, and neutralize scam operations.

## 🎯 Mission

To create a safer digital environment for Malaysians by:
- **Detecting** scams in real-time across messaging platforms
- **Protecting** vulnerable communities through automated warnings
- **Disrupting** scammer operations through ethical countermeasures
- **Educating** users about emerging scam tactics

## ✨ Key Features

### 🔍 Advanced Scam Detection
- Multi-language support (Malay, English, Mandarin, Tamil)
- Pattern recognition for Malaysian-specific scams
- Real-time threat analysis
- Machine learning-based classification

### 📱 WhatsApp Integration
- Full WhatsApp Web functionality via Baileys
- Group monitoring and protection
- Automated scam warnings
- Media analysis (images, documents, links)

### 🤖 Intelligent Response System
- Sandboxed scambaiter with multiple personas
- Time-wasting strategies to disrupt scammers
- Automated evidence collection
- Safe engagement protocols

### 📊 Analytics & Reporting
- Real-time dashboard
- Scammer network mapping
- Trend analysis
- Automated reporting to authorities

### 🔒 Security & Privacy
- Automatic PII redaction
- End-to-end encryption for sensitive data
- Audit logging with immutable records
- GDPR/PDPA compliant

## 🚀 Quick Start

### Prerequisites
- Docker & Docker Compose
- Python 3.11+
- Node.js 18+ (for Baileys)
- PostgreSQL 15+
- Redis 7+

### Installation

```bash
# Clone repository
git clone https://gitlab.com/Behelit-Systems/the-juara-rakyat.git
cd the-juara-rakyat

# Copy environment configuration
cp .env.example .env
# Edit .env with your configuration

# Start services with Docker Compose
docker-compose up -d

# Initialize database
make db-migrate

# Start the platform
make run

# Access dashboard at http://localhost:3000