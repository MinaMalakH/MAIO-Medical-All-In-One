# 🏥 MAIO - Medical Appointment Integration Online

[![Node.js](https://img.shields.io/badge/Node.js-18+-green?logo=node.js)](https://nodejs.org/)
[![React](https://img.shields.io/badge/React-19.2-blue?logo=react)](https://react.dev/)
[![Next.js](https://img.shields.io/badge/Next.js-16.0-black?logo=next.js)](https://nextjs.org/)
[![MongoDB](https://img.shields.io/badge/MongoDB-9.0-green?logo=mongodb)](https://www.mongodb.com/)
[![License](https://img.shields.io/badge/License-ISC/MIT-blue)](#license)

**MAIO** is a comprehensive, enterprise-grade telemedicine platform connecting patients, doctors, and healthcare administrators. It features real-time communication, secure payment processing, intelligent appointment scheduling, and complete medical records management.

This repository contains the complete monorepo structure with three main applications:

---

## 📁 Project Overview

```
MAIO/
├── MAIO-Backend/          # Express.js REST API & WebSocket server
├── MAIO-front/            # React patient/doctor portal
├── maiodashboard/         # Next.js admin dashboard
└── README.md             # This file
```

### What is MAIO?

MAIO bridges the gap between patients and healthcare providers through:

✅ **Seamless Appointment Booking** - Real-time availability with instant confirmation  
✅ **Secure Telemedicine** - Real-time chat and video consultation support  
✅ **Medical Records Management** - Centralized patient health data and prescriptions  
✅ **Integrated Payments** - Stripe-powered secure payment processing  
✅ **Admin Dashboard** - Complete platform management and analytics  
✅ **Scalable Architecture** - Production-ready microservices approach

---

## 🎯 Quick Start

### Option 1: Run All Services (Recommended for Development)

```bash
# Terminal 1: Backend Service
cd MAIO-Backend
npm install
npm start
# Server runs on http://localhost:5000

# Terminal 2: Patient/Doctor Portal
cd MAIO-front
npm install
npm run dev
# Frontend runs on http://localhost:5173

# Terminal 3: Admin Dashboard
cd maiodashboard
npm install
npm run dev
# Dashboard runs on http://localhost:3000
```

### Option 2: Using Docker (Coming Soon)

```bash
docker-compose up -d
```

---

## 📚 Detailed Documentation

### Backend API

Complete backend documentation with setup instructions, API endpoints, database schemas, and WebSocket implementation.

→ [MAIO-Backend README](MAIO-Backend/README.md)

**Key Features:**

- Express.js 5.2 REST API
- MongoDB database with Mongoose ORM
- JWT authentication & role-based access control
- Socket.io real-time communication
- Stripe payment integration
- Nodemailer email service
- Multi-file upload with Multer

---

### Patient & Doctor Portal

React-based frontend for patient appointment booking, medical history management, real-time doctor consultation, and payment processing.

→ [MAIO-Front README](MAIO-front/README.md)

**Key Features:**

- React 19.2 with TypeScript
- Vite ultra-fast build tool
- TanStack React Query for server state
- Redux Toolkit for global state
- Stripe payment integration
- Socket.io real-time messaging
- Responsive design with Tailwind CSS & DaisyUI

---

### Admin Dashboard

Next.js-based administration platform for managing users, verifying doctors, tracking appointments, and viewing platform analytics.

→ [Admin Dashboard README](maiodashboard/README.md)

**Key Features:**

- Next.js 16.0 framework
- Server-side rendering & static generation
- Comprehensive user management
- Doctor verification workflow
- Dashboard metrics & analytics
- Tailwind CSS for styling

---

## 🏗️ Architecture Overview

### System Architecture

```
┌─────────────────────────────────────────────────────────┐
│                   Client Layer                           │
├──────────────────┬──────────────────┬──────────────────┤
│ Patient Portal   │ Doctor Portal    │ Admin Dashboard  │
│  (MAIO-front)    │  (MAIO-front)    │ (maiodashboard)  │
└──────────┬───────┴────────┬─────────┴──────────┬────────┘
           │                │                    │
           │  REST API      │  WebSocket         │
           │  HTTP/HTTPS    │  Socket.io         │
           └────────┬───────┴────────┬───────────┘
                    │                │
        ┌───────────▼────────────────▼────────────┐
        │   MAIO Backend (API Server)             │
        │   Express.js 5.2 + Node.js              │
        │   - Authentication & Authorization      │
        │   - Business Logic & Controllers        │
        │   - WebSocket Server                    │
        │   - File Upload Handler                 │
        │   - Payment Processing                  │
        │   - Email Service                       │
        └───────────┬────────────────────────────┘
                    │
        ┌───────────▼────────────────────────────┐
        │   Data & External Services             │
        ├────────────┬────────────┬──────────────┤
        │  MongoDB   │  Stripe    │  Nodemailer  │
        │  Database  │  Payments  │  Email       │
        └────────────┴────────────┴──────────────┘
```

### Technology Stack Summary

| Layer              | Technology        | Version |
| ------------------ | ----------------- | ------- |
| **Backend API**    | Node.js + Express | 5.2     |
| **Database**       | MongoDB           | 9.0+    |
| **Frontend**       | React             | 19.2    |
| **Admin**          | Next.js           | 16.0    |
| **Real-time**      | Socket.io         | 4.8+    |
| **Styling**        | Tailwind CSS      | 4.1     |
| **Authentication** | JWT               | -       |
| **Payments**       | Stripe            | 20.1+   |

---

## 📋 Features Breakdown

### 🔐 User Management

- **Patient Registration**: Medical history, allergies, emergency contacts
- **Doctor Registration**: Verification documents, specialization, experience
- **Admin Accounts**: Full platform access and management
- **Role-Based Access Control**: Granular permission system
- **Profile Management**: Complete user profile editing

### 🏥 Appointment System

- **Smart Availability**: Real-time slot availability
- **Calendar Integration**: Interactive appointment scheduling
- **Automatic Confirmation**: Email notifications
- **Status Tracking**: Real-time appointment status
- **Cancellation & Rescheduling**: Flexible appointment management

### 💬 Real-Time Communication

- **Live Chat**: WebSocket-based messaging
- **Typing Indicators**: Real-time typing status
- **Online Status**: User availability detection
- **Message History**: Persistent conversation storage
- **Notifications**: Real-time alerts for events

### 📄 Medical Records

- **Medical History**: Comprehensive patient health records
- **Prescription Management**: Digital prescriptions
- **Document Storage**: Secure file uploads
- **Health Metrics**: Vital signs and measurements
- **Document Search**: Quick access to records

### 💳 Payment Processing

- **Stripe Integration**: Secure payment gateway
- **Multiple Payment Methods**: Credit/debit card support
- **Invoice Generation**: Automated receipts
- **Payment History**: Transaction tracking
- **Refund Management**: Easy refund processing

### 📊 Analytics & Dashboard

- **Key Metrics**: Real-time platform statistics
- **User Analytics**: Registration and engagement tracking
- **Appointment Analytics**: Booking trends and patterns
- **Revenue Tracking**: Payment analytics
- **Doctor Performance**: Consultation metrics

---

## 🚀 Deployment

### Development Environment

All three services run locally on different ports for development:

- **Backend**: http://localhost:5000
- **Frontend**: http://localhost:5173
- **Admin**: http://localhost:3000

### Production Deployment

#### Backend (Heroku/Railway)

```bash
cd MAIO-Backend
git push heroku main
```

#### Frontend (Vercel/Netlify)

```bash
# Vercel (Recommended for Next.js)
cd MAIO-front
vercel deploy
```

#### Admin Dashboard (Vercel)

```bash
cd maiodashboard
vercel deploy
```

### Environment Variables

Each service requires specific environment variables. See individual README files for detailed configuration.

---

## 🤝 Contributing

### Getting Started with Development

1. **Fork the Repository**

   ```bash
   git clone https://github.com/your-username/MAIO.git
   cd MAIO
   ```

2. **Create Feature Branch**

   ```bash
   git checkout -b feature/amazing-feature
   ```

3. **Make Changes**

   - Follow code style guidelines
   - Write descriptive commit messages
   - Add comments for complex logic

4. **Commit & Push**

   ```bash
   git commit -m 'Add amazing feature'
   git push origin feature/amazing-feature
   ```

5. **Open Pull Request**
   - Describe your changes
   - Reference related issues
   - Wait for code review

### Code Style & Standards

- **Backend**: Node.js/Express.js best practices
- **Frontend**: React hooks and functional components
- **Admin**: Next.js app router conventions
- **Language**: English for all code comments and documentation

### Testing

Each service should include tests:

- Unit tests for business logic
- Integration tests for APIs
- Component tests for UI

---

## 🔒 Security Considerations

### Authentication & Authorization

- JWT tokens with secure refresh mechanism
- HTTP-only cookies for token storage
- Role-based access control (RBAC)
- Secure password hashing with bcryptjs

### Data Protection

- HTTPS/TLS encryption in transit
- Database encryption at rest
- Sensitive data masking in logs
- GDPR-compliant soft deletion

### API Security

- Request rate limiting
- Input validation & sanitization
- CORS configuration
- SQL injection prevention
- XSS protection with Helmet.js

### Payment Security

- PCI-DSS compliance via Stripe
- No sensitive card data stored
- Secure PaymentIntent handling
- Webhook signature verification

---

## 📞 Support & Contact

### Issue Reporting

- **Bugs**: Create issue with reproduction steps
- **Features**: Describe use case and expected behavior
- **Documentation**: Report unclear or missing documentation

### Community Channels

- GitHub Issues: Bug reports and feature requests
- GitHub Discussions: General questions and ideas
- Email: support@maio-health.com (if applicable)

---

## 📜 License

### MAIO-Backend

Licensed under **ISC License**

### MAIO-Front & Admin Dashboard

Licensed under **MIT License**

See individual LICENSE files in each directory for details.

---

## 🗂️ Repository Structure

```
MAIO/
│
├── MAIO-Backend/                    # Node.js Express API
│   ├── controllers/                # Business logic
│   ├── models/                     # MongoDB schemas
│   ├── routes/                     # API endpoints
│   ├── middleware/                 # Auth, validation, etc.
│   ├── services/                   # External integrations
│   ├── sockets/                    # WebSocket handlers
│   ├── config/                     # Configuration files
│   ├── package.json
│   └── README.md                   # Backend documentation
│
├── MAIO-front/                      # React Patient/Doctor Portal
│   ├── src/
│   │   ├── features/               # Feature modules
│   │   ├── pages/                  # Page components
│   │   ├── services/               # API services
│   │   ├── hooks/                  # Custom hooks
│   │   ├── store/                  # Redux configuration
│   │   ├── ui/                     # Reusable UI components
│   │   └── utils/                  # Utility functions
│   ├── package.json
│   ├── vite.config.ts
│   └── README.md                   # Frontend documentation
│
├── maiodashboard/                   # Next.js Admin Dashboard
│   ├── app/
│   │   ├── dashboard/              # Dashboard pages
│   │   ├── users/                  # User management
│   │   ├── doctors/                # Doctor management
│   │   ├── appointments/           # Appointment tracking
│   │   ├── components/             # Shared components
│   │   └── layout.js               # App layout
│   ├── lib/                        # Utility functions
│   ├── hooks/                      # Custom hooks
│   ├── package.json
│   ├── next.config.mjs
│   └── README.md                   # Admin documentation
│
└── README.md                         # This file (main documentation)
```

---

## 📈 Project Roadmap

### Phase 1: MVP (Current)

- ✅ Patient appointment booking
- ✅ Doctor profile management
- ✅ Real-time messaging
- ✅ Payment processing
- ✅ Admin dashboard basics

### Phase 2: Q2 2026

- 🔄 Video consultation integration
- 🔄 Advanced scheduling algorithms
- 🔄 Mobile app (React Native)
- 🔄 Multi-language support

### Phase 3: Q3 2026

- 📋 AI-powered doctor recommendations
- 📋 Insurance verification system
- 📋 Advanced analytics & reporting
- 📋 Prescription fulfillment integration

### Phase 4: Q4 2026

- 🎯 Telemedicine network expansion
- 🎯 Blockchain for records (optional)
- 🎯 International expansion
- 🎯 Enterprise features

---

## 📊 Project Statistics

| Component | Lines of Code | Files    | Dependencies |
| --------- | ------------- | -------- | ------------ |
| Backend   | ~5,000        | 50+      | 12           |
| Frontend  | ~4,500        | 60+      | 25+          |
| Admin     | ~2,000        | 35+      | 8            |
| **Total** | **~11,500**   | **145+** | **45+**      |

---

## 🙏 Acknowledgments

Special thanks to:

- The open-source community
- All contributors
- Users and testers providing feedback

---

## 📧 Contact

- **Email**: contact@maio-health.com
- **Website**: https://maio-health.com
- **GitHub**: https://github.com/your-username/MAIO
- **Issues**: https://github.com/your-username/MAIO/issues

---

## 🎓 Learning Resources

### Backend Development

- [Express.js Documentation](https://expressjs.com/)
- [MongoDB & Mongoose](https://www.mongodb.com/)
- [Socket.io Guide](https://socket.io/docs/)
- [Stripe API Reference](https://stripe.com/docs/api)

### Frontend Development

- [React Documentation](https://react.dev/)
- [Vite User Guide](https://vitejs.dev/)
- [Tailwind CSS Docs](https://tailwindcss.com/docs)
- [React Query Guide](https://tanstack.com/query/latest/)

### Admin Dashboard

- [Next.js Documentation](https://nextjs.org/docs)
- [App Router Guide](https://nextjs.org/docs/app)
- [TypeScript Guide](https://www.typescriptlang.org/docs/)

---

<div align="center">

### Made with ❤️ for better healthcare delivery

**[Live Demo](#)** · **[Report Bug](#)** · **[Request Feature](#)** · **[Contributing](#)**

**Last Updated**: January 2026 | **Version**: 1.0.0

</div>
