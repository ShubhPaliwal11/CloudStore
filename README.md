# Cloud Store

<div align="center">
  <img src="public\assets\images\cloud.png" alt="Cloud Store Logo" width="200">
  
  <h3>Modern Cloud Storage & File Sharing Platform</h3>
  
  <div>
    <img src="https://img.shields.io/badge/-Next_JS_15-black?style=for-the-badge&logoColor=white&logo=nextdotjs&color=000000" alt="Next.js" />
    <img src="https://img.shields.io/badge/-TypeScript-black?style=for-the-badge&logoColor=white&logo=typescript&color=3178C6" alt="TypeScript" />
    <img src="https://img.shields.io/badge/-Tailwind_CSS-black?style=for-the-badge&logoColor=white&logo=tailwindcss&color=06B6D4" alt="Tailwind CSS" />
    <img src="https://img.shields.io/badge/-Supabase-black?style=for-the-badge&logoColor=white&logo=supabase&color=3ECF8E" alt="Supabase" />
  </div>
</div>

---

## 📋 Table of Contents

1. [Introduction](#-introduction)
2. [Features](#-features)
3. [Tech Stack](#️-tech-stack)
4. [Quick Start](#-quick-start)
5. [Environment Variables](#-environment-variables)
6. [Database Setup](#-database-setup)

---

## 🤖 Introduction

**Cloud Store** is a modern storage management and file sharing platform that lets users effortlessly upload, organize, and share files. Built with Next.js 15 and Supabase, it provides a seamless cloud storage experience with a beautiful, responsive interface.

---

## 🔋 Features

- **🔐 User Authentication** - Secure email/password authentication with Supabase Auth
- **📁 File Uploads** - Upload documents, images, videos, and audio files
- **👁️ View & Manage Files** - Browse, preview, rename, and delete your files
- **⬇️ Download Files** - Instant access to download any uploaded file
- **🔗 File Sharing** - Share files with other users via email
- **📊 Dashboard** - Visual overview of storage usage with charts
- **🔍 Global Search** - Quickly find files across your storage
- **🔄 Sorting Options** - Sort by date, name, or file size
- **📱 Responsive Design** - Works beautifully on desktop and mobile

---

## ⚙️ Tech Stack

| Technology | Purpose |
|------------|---------|
| **Next.js 15** | React framework with App Router |
| **React 19** | UI library |
| **TypeScript** | Type safety |
| **Supabase** | Authentication, Database & Storage |
| **Tailwind CSS** | Styling |
| **ShadCN UI** | UI components |
| **Recharts** | Dashboard charts |

---

## 🚀 Quick Start

### Prerequisites

- [Node.js](https://nodejs.org/) (v18 or higher)
- [npm](https://www.npmjs.com/) or [yarn](https://yarnpkg.com/)
- [Supabase Account](https://supabase.com/)

### Installation

1. **Clone the repository**
   ```bash
   git clone <your-repo-url>
   cd cloud-store
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```

3. **Set up environment variables**
   
   Create a `.env.local` file in the root directory:
   ```env
   NEXT_PUBLIC_SUPABASE_URL="your-supabase-project-url"
   NEXT_PUBLIC_SUPABASE_ANON_KEY="your-supabase-anon-key"
   NEXT_PUBLIC_SUPABASE_BUCKET="files"
   SUPABASE_SERVICE_ROLE_KEY="your-supabase-service-role-key"
   ```

4. **Run the development server**
   ```bash
   npm run dev
   ```

5. **Open in browser**
   
   Navigate to [http://localhost:3000](http://localhost:3000)

---

## 🔑 Environment Variables

| Variable | Description |
|----------|-------------|
| `NEXT_PUBLIC_SUPABASE_URL` | Your Supabase project URL |
| `NEXT_PUBLIC_SUPABASE_ANON_KEY` | Public/anon API key |
| `NEXT_PUBLIC_SUPABASE_BUCKET` | Storage bucket name (default: `files`) |
| `SUPABASE_SERVICE_ROLE_KEY` | Service role key (keep secret!) |

**Finding your credentials:**
1. Go to your Supabase Dashboard
2. Navigate to **Project Settings** → **API**
3. Copy the values from the API page

---

## 🗄️ Database Setup

### Users Table

```sql
CREATE TABLE users (
  id UUID DEFAULT gen_random_uuid() PRIMARY KEY,
  full_name TEXT NOT NULL,
  email TEXT UNIQUE NOT NULL,
  avatar TEXT,
  account_id TEXT,
  created_at TIMESTAMPTZ DEFAULT NOW(),
  updated_at TIMESTAMPTZ DEFAULT NOW()
);
```

### Files Table

```sql
CREATE TABLE files (
  id UUID DEFAULT gen_random_uuid() PRIMARY KEY,
  type TEXT NOT NULL,
  name TEXT NOT NULL,
  url TEXT NOT NULL,
  extension TEXT,
  size BIGINT NOT NULL,
  owner UUID REFERENCES users(id),
  account_id TEXT,
  users TEXT[] DEFAULT '{}',
  bucket_file_id TEXT NOT NULL,
  created_at TIMESTAMPTZ DEFAULT NOW(),
  updated_at TIMESTAMPTZ DEFAULT NOW()
);
```

### Storage Bucket

1. Go to **Storage** in your Supabase Dashboard
2. Create a new bucket named `files`
3. Set the bucket to **Public**

### Authentication Settings

1. Go to **Authentication** → **Providers** → **Email**
2. Disable **"Confirm email"** for development
3. Set **Site URL** to `http://localhost:3000`

---

## 📁 Project Structure

```
cloud-store/
├── app/                    # Next.js App Router
│   ├── (auth)/            # Auth pages (sign-in, sign-up)
│   ├── (root)/            # Protected pages (dashboard, files)
│   └── layout.tsx         # Root layout
├── components/            # React components
│   ├── ui/               # ShadCN UI components
│   └── ...               # Feature components
├── lib/                   # Utilities and actions
│   ├── actions/          # Server actions
│   └── supabase/         # Supabase client
├── public/               # Static assets
└── types/                # TypeScript types
```

---

## 📄 License

This project is open source and available under the [MIT License](LICENSE).

---

<div align="center">
  <p>Built with ❤️ using Next.js and Supabase</p>
</div>
