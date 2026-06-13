# 📚 The Literary Shelf

> A modern virtual library platform for students to donate and borrow books.
> *Initiated by Rupali and Sarayu of Class 11B*

---

## 🌟 Overview

**The Literary Shelf** is an interactive web application designed as a virtual library for school students. It enables students to:

- 📖 **Browse** available donated books and request to borrow them
- 🎁 **Donate** books they no longer need
- 📝 **Request** specific books they are looking for
- 👤 **Create a profile** to track their activity

The website features a contemporary library aesthetic with glassmorphism design, parallax effects, and an AI helper mascot named **Sara** — a school girl holding a book who provides interactive tips.

---

## 🎨 Design Features

### Visual Style
- **Glassmorphism**: Translucent cards and panels with backdrop blur effects
- **Parallax Scrolling**: Multi-layer depth effects on the hero section
- **Contemporary Library Theme**: Warm amber and teal color palette evoking a modern reading space
- **Responsive Design**: Fully adaptive across desktop, tablet, and mobile devices

### Color Palette
- Primary: Amber/Gold tones for warmth and readability
- Secondary: Teal accents for interactive elements
- Background: Deep navy with subtle gradients
- Glass surfaces: Semi-transparent white with blur

---

## 🏗️ Architecture

### Tech Stack
| Layer | Technology |
|-------|------------|
| Framework | TanStack Start (React 19 + Vite 7) |
| Styling | Tailwind CSS v4 with custom design tokens |
| Backend | Lovable Cloud (Supabase) |
| Auth | Email + Google OAuth |
| Database | PostgreSQL with Row Level Security (RLS) |
| Notifications | Sonner toast notifications |

### Database Schema

#### Tables
1. **`profiles`**
   - `id` (uuid, PK) — linked to auth.users
   - `username` (text)
   - `full_name` (text)
   - `class_section` (text) — e.g., "11B"
   - `avatar_url` (text)
   - `updated_at` (timestamp)

2. **`books`**
   - `id` (uuid, PK)
   - `title` (text)
   - `author` (text)
   - `subject` (text)
   - `condition` (enum: new, good, fair, worn)
   - `donor_id` (uuid, FK → profiles)
   - `is_available` (boolean)
   - `notes` (text)
   - `created_at` (timestamp)

3. **`borrow_requests`**
   - `id` (uuid, PK)
   - `book_id` (uuid, FK → books)
   - `requester_id` (uuid, FK → profiles)
   - `status` (enum: pending, approved, rejected, returned)
   - `created_at` (timestamp)

4. **`book_requests`** (Wishlist)
   - `id` (uuid, PK)
   - `title` (text)
   - `author` (text, optional)
   - `subject` (text)
   - `requester_id` (uuid, FK → profiles)
   - `notes` (text)
   - `created_at` (timestamp)

### Security
- **Row Level Security (RLS)** enabled on all tables
- Policies ensure users can only access their own data or public information
- Authentication required for donating, borrowing, and requesting books

---

## 📄 Pages

### 1. Home (`/`)
The landing page featuring:
- Parallax hero section with library imagery
- Introduction to the platform's mission
- Three core pillars: Donate, Borrow, Request
- Animated mascot (Sara) with helpful tips

### 2. Browse (`/browse`)
- Searchable catalog of all available donated books
- Filter by subject, condition, or availability
- Request-to-borrow functionality for each book

### 3. Donate (`/donate`)
- Form to list a book for donation
- Fields: Title, Author, Subject, Condition, Notes
- Books immediately become available for others to borrow

### 4. Request (`/request`)
- Wishlist page for requesting specific books
- Students can add titles they're looking for
- Community members can see requests and donate matching books

### 5. Profile (`/profile`)
- User activity dashboard
- Tracks donated books count, borrowed books count
- Editable class section and personal details
- List of active borrow requests

### 6. About Us (`/about`)
- Project credits: **Rupali and Sarayu of Class 11B**
- Mission statement about promoting reading and resource sharing
- Call to action for participation

### 7. Auth (`/auth`)
- Login / Sign-up page
- Email/password authentication
- Google OAuth option

---

## 🤖 AI Mascot — Sara

Sara is an animated school girl holding a book who appears across the site:
- **Animations**: Gentle bobbing motion (`animate-mascot-bob`)
- **Interactivity**: Provides contextual tips based on the current page
- **Design**: Friendly, approachable character reinforcing the educational theme

---

## 🚀 Getting Started

### Prerequisites
- Node.js (v20+)
- Bun or npm

### Installation
```bash
# Install dependencies
bun install

# Start development server
bun run dev
```

### Environment Variables
```env
VITE_SUPABASE_URL=your_supabase_url
VITE_SUPABASE_PUBLISHABLE_KEY=your_anon_key
```

---

## 🙏 Credits

- **Project Initiators**: Rupali and Sarayu, Class 11B
- **Purpose**: School library resource sharing initiative
- **Built with**: Lovable + TanStack Start + Tailwind CSS

---

## 📜 License

This project is built for educational and school community purposes.

---

*Made with ❤️ for the love of books and learning.*
