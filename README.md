# Confessio - Anonymous Forum Platform

Confessio adalah platform forum anonim yang memungkinkan pengguna untuk berbagi pemikiran, pengalaman, dan berinteraksi dalam lingkungan yang aman dan tanpa identitas. Dibangun dengan Next.js 15, TypeScript, dan Supabase.

✨ Fitur Utama

🔒 **Anonymous First**
- Tidak perlu registrasi atau login
- Semua interaksi bersifat anonim
- Privasi pengguna terjaga sepenuhnya

🏠 **Room System**
- Buat room diskusi dengan topik tertentu
- Semua room bersifat publik dan terbuka
- Search dan filter room dengan mudah

💬 **Real-time Messaging**
- Kirim pesan dalam room secara real-time
- Thread replies dengan visual connector
- Reaction system untuk setiap pesan

🎨 **Modern UI/UX**
- Dark/Light theme toggle
- Responsive design untuk semua device
- Smooth animations dan transitions
- Clean dan intuitive interface

🛠️ Tech Stack

Frontend
- **Next.js 15** - React framework dengan App Router
- **TypeScript** - Type-safe development
- **Tailwind CSS** - Utility-first CSS framework
- **shadcn/ui** - Modern UI components
- **Lucide React** - Beautiful icons

Backend
- **Next.js API Routes** - Serverless API endpoints
- **Supabase** - Backend-as-a-Service
- **PostgreSQL** - Relational database

Development Tools
- **ESLint** - Code linting
- **Prettier** - Code formatting
- **PostCSS** - CSS processing

🚀 Quick Start

Prerequisites
- Node.js 18+ 
- npm/yarn/pnpm
- Supabase account (untuk production)

Installation

1. **Clone repository**
\`\`\`bash
git clone (https://github.com/Repyandika/Anon-Forum)
cd confessio
\`\`\`

2. **Install dependencies**
\`\`\`bash
npm install
# atau
yarn install
# atau
pnpm install
\`\`\`

3. **Setup environment variables**
\`\`\`bash
cp .env.example .env.local
\`\`\`

Edit `.env.local`:
\`\`\`env
NEXT_PUBLIC_SUPABASE_URL=your_supabase_url
NEXT_PUBLIC_SUPABASE_ANON_KEY=your_supabase_anon_key
SUPABASE_SERVICE_ROLE_KEY=your_service_role_key
\`\`\`

4. **Setup database**
\`\`\`bash
# Jalankan SQL scripts di Supabase Dashboard
# atau gunakan Supabase CLI
supabase db reset
\`\`\`

5. **Run development server**
\`\`\`bash
npm run dev
# atau
yarn dev
# atau
pnpm dev
\`\`\`

Buka [http://localhost:3000](http://localhost:3000) di browser.

📁 Project Structure

\`\`\`
confessio/
├── app/                    # Next.js App Router
│   ├── api/               # API routes
│   │   ├── rooms/         # Room management
│   │   ├── messages/      # Message handling
│   │   ├── reactions/     # Reaction system
│   │   └── replies/       # Reply system
│   ├── room/[id]/         # Dynamic room pages
│   ├── profile/[username]/ # User profiles
│   └── globals.css        # Global styles
├── components/            # React components
│   ├── ui/               # shadcn/ui components
│   ├── forms/            # Form components
│   ├── rooms/            # Room-related components
│   ├── messages/         # Message components
│   ├── reactions/        # Reaction components
│   └── replies/          # Reply components
├── lib/                  # Utility libraries
│   ├── supabase.ts       # Supabase client
│   └── utils.ts          # Helper functions
├── hooks/                # Custom React hooks
├── scripts/              # Database scripts
└── public/               # Static assets
\`\`\`

🗄️ Database Schema

Tables

 `rooms`
\`\`\`sql
CREATE TABLE rooms (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  name VARCHAR(255) NOT NULL,
  description TEXT,
  is_private BOOLEAN DEFAULT false,
  created_at TIMESTAMP DEFAULT NOW()
);
\`\`\`

`messages`
\`\`\`sql
CREATE TABLE messages (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  content TEXT NOT NULL,
  username VARCHAR(100),
  created_at TIMESTAMP DEFAULT NOW()
);
\`\`\`

`room_messages`
\`\`\`sql
CREATE TABLE room_messages (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  room_id UUID REFERENCES rooms(id) ON DELETE CASCADE,
  content TEXT NOT NULL,
  username VARCHAR(100),
  created_at TIMESTAMP DEFAULT NOW()
);
\`\`\`

`room_message_replies`
\`\`\`sql
CREATE TABLE room_message_replies (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  message_id UUID REFERENCES room_messages(id) ON DELETE CASCADE,
  content TEXT NOT NULL,
  username VARCHAR(100),
  image_url TEXT,
  created_at TIMESTAMP DEFAULT NOW()
);
\`\`\`

`reactions`
\`\`\`sql
CREATE TABLE reactions (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  message_id UUID,
  emoji VARCHAR(10) NOT NULL,
  count INTEGER DEFAULT 1,
  created_at TIMESTAMP DEFAULT NOW()
);
\`\`\`

 🎯 API Endpoints

 Rooms
- `GET /api/rooms` - Get all rooms with search
- `POST /api/rooms` - Create new room
- `GET /api/rooms/[id]` - Get specific room

 Messages
- `GET /api/messages` - Get all messages
- `POST /api/messages` - Create new message
- `GET /api/room-messages?room_id=` - Get room messages
- `POST /api/room-messages` - Create room message

 Replies
- `GET /api/replies?message_id=` - Get message replies
- `POST /api/replies` - Create new reply

 Reactions
- `GET /api/reactions?message_id=` - Get message reactions
- `POST /api/reactions` - Add/update reaction

 🎨 UI Components

 Core Components
- `Navigation` - Main navigation menu
- `Footer` - Footer dengan developer info
- `ThemeToggle` - Dark/light mode switcher

 Form Components
- `CreateRoomForm` - Form untuk membuat room baru
- `SendMessageForm` - Form untuk mengirim pesan
- `SendRoomMessageForm` - Form untuk pesan di room

 Feature Components
- `RoomList` - Daftar room dengan search
- `MessageList` - Daftar pesan dengan reactions
- `MessageReplies` - Thread replies dengan visual connector
- `MessageReactions` - Reaction buttons dan counter

 🔧 Configuration

 Tailwind CSS
Custom configuration dengan:
- Dark mode support
- Custom colors dan gradients
- Animation utilities
- Responsive breakpoints

 Next.js
- App Router configuration
- API routes setup
- Image optimization
- TypeScript strict mode

 🚀 Deployment

 Vercel (Recommended)
1. Push ke GitHub repository
2. Connect ke Vercel
3. Set environment variables
4. Deploy automatically

 Manual Deployment
\`\`\`bash
npm run build
npm start
\`\`\`

📝 License

Distributed under the MIT License. See `LICENSE` for more information.




🔗 Links

Live Demo: [https://confessio.vercel.app](https://confessio.vercel.app)

Made with ❤️ by Confessio Team

Confessio - Where thoughts flow freely, anonymously.
