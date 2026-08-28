
# GIA Guía Inteligente de Instalación

![Python](https://img.shields.io/badge/Python-3.12-3776AB?style=flat&logo=python&logoColor=white)
![Flask](https://img.shields.io/badge/Flask-3.0-000000?style=flat&logo=flask&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-16-4169E1?style=flat&logo=postgresql&logoColor=white)
![SQLAlchemy](https://img.shields.io/badge/SQLAlchemy-2.0-D71F00?style=flat&logo=sqlalchemy&logoColor=white)
![React](https://img.shields.io/badge/React-18-61DAFB?style=flat&logo=react&logoColor=black)
![Vite](https://img.shields.io/badge/Vite-5-646CFF?style=flat&logo=vite&logoColor=white)
![TailwindCSS](https://img.shields.io/badge/Tailwind-3-06B6D4?style=flat&logo=tailwindcss&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-ES2024-F7DF1E?style=flat&logo=javascript&logoColor=black)
![Groq](https://img.shields.io/badge/Groq-LPU-FF6C2F?style=flat&logo=groq&logoColor=white)
![Anthropic](https://img.shields.io/badge/Anthropic-Claude-D4A574?style=flat&logo=anthropic&logoColor=white)
![Cloudinary](https://img.shields.io/badge/Cloudinary-Media-3448C5?style=flat&logo=cloudinary&logoColor=white)
![Vercel](https://img.shields.io/badge/Vercel-Deploy-000000?style=flat&logo=vercel&logoColor=white)
![Render](https://img.shields.io/badge/Render-Backend-46E3B7?style=flat&logo=render&logoColor=white)
![JWT](https://img.shields.io/badge/JWT-Auth-000000?style=flat&logo=jsonwebtokens&logoColor=white)

> Asistente de IA para montar, instalar, reparar y restaurar productos del hogar.

---

## ¿Qué es GIA?

GIA nace de una experiencia real montar un mueble durante una mudanza, con el manual delante, y no entender nada. La idea es simple que cualquier persona pueda recibir ayuda experta paso a paso, como si tuviera a un técnico al lado.

GIA guía al usuario desde el primer mensaje hasta el último tornillo. Analiza manuales en PDF, interpreta fotografías, recuerda el progreso y adapta su lenguaje al nivel de cada persona.

---

## Funcionalidades actuales

### Chat con IA
- Conversación natural en español con GIA
- Respuestas adaptadas al nivel del usuario (principiante, intermedio, experto)
- Memoria de contexto GIA recuerda el proyecto, las piezas y el progreso
- Dictado de voz integrado
- Renombrar conversaciones directamente desde el chat

### Análisis de manuales PDF
- Subida de PDF directamente en el chat
- Extracción automática de inventario: piezas, herrajes, herramientas, pasos
- GIA usa el inventario para identificar piezas por nombre y letra durante el montaje
- Chunking inteligente para no consumir tokens innecesarios

### Análisis visual de imágenes
- El usuario envía una foto del producto o del problema
- GIA analiza la imagen y responde con contexto del proyecto activo
- Compatible con fotos desde móvil (JPG, PNG, WEBP, HEIC)

### Seguimiento de proyectos
- Barra de progreso actualizada automáticamente según los pasos completados
- Estados: en progreso / completado
- Historial de conversaciones por proyecto
- Renombrar proyectos directamente desde el chat

### Acciones rápidas desde el Home
- Instalar un producto (TV, lámparas, ventiladores, aires)
- Reparar un producto (electrodomésticos, radiadores, lavadoras, neveras)
- Reparar / Restaurar mueble (segunda vida para muebles dañados o antiguos)
- Montaje de mueble (nuevo o antiguo, paso a paso)

### Diseño y experiencia
- Interfaz minimalista escandinava (paleta inspirada en Muuto/HAY)
- Modo claro / oscuro con persistencia
- Responsive completo diseñado para móvil y desktop
- Tab bar nativo en móvil, sidebar fijo en desktop
- Imágenes nórdicas ilustrativas generadas con IA

---

## Stack técnico

| Capa | Tecnología |
|------|-----------|
| Frontend | React + Vite + Tailwind CSS + shadcn/ui |
| Backend | Flask (Python 3.12) + PostgreSQL + SQLAlchemy + Alembic |
| IA Chat | Groq|
| IA PDFs | Anthropic Claude Haiku (chunking y extracción) |
| IA Imágenes | Anthropic Claude (análisis visual) |
| Almacenamiento imágenes | Cloudinary |
| Auth | JWT + Werkzeug |
| Deploy Frontend | Vercel |
| Deploy Backend | Render |

---

## Arquitectura

```
Usuario
  │
  ├── Frontend (React/Vercel)
  │     ├── Home — dashboard con proyectos y acciones rápidas
  │     ├── Chat — conversación con GIA
  │     ├── Proyectos — historial con barra de progreso
  │     ├── Manuales — proyectos con PDF analizado
  │     └── Nuevo proyecto — flujo de creación
  │
  └── Backend (Flask/Render)
        ├── /api/chat — conversación principal con Groq
        ├── /api/chat/image — análisis visual con Anthropic
        ├── /api/manuals/:id/upload — procesamiento PDF con Anthropic
        ├── /api/conversations — CRUD de proyectos
        ├── /api/auth — registro y login JWT
        └── /api/health — keepalive para Render Free
```

**Principio de arquitectura:** un agente, un objetivo. Cada endpoint tiene una responsabilidad clara y no se mezclan capas.

---

## Instalación local

### Requisitos
- Python 3.12
- Node.js 18+
- PostgreSQL
- Pipenv

### Backend

```bash
git clone https://github.com/genesisfalcon15-alt/GIA
cd GIA/src
pipenv install
cp .env.example .env  # configura tus variables
pipenv run flask --app app run --host=0.0.0.0 --port=3001 --debug
```

### Frontend

```bash
cd GIA
npm install
npm run dev
```

### Variables de entorno necesarias

```env
# Backend (.env en /src)
FLASK_APP=app
FLASK_APP_KEY=tu_secret_key
DATABASE_URL=postgresql://...
GROQ_API_KEY=...
ANTHROPIC_API_KEY=...
CLOUDINARY_CLOUD_NAME=...
CLOUDINARY_API_KEY=...
CLOUDINARY_API_SECRET=...

# Frontend (.env en raíz)
VITE_BACKEND_URL=http://localhost:3001
```

---

## Roadmap — próximas versiones

### v1.1 — Mejoras de experiencia
- [ ] Pregunta de confirmación de paso con actualización automática de progreso
- [ ] Biblioteca de guías — catálogo visual de proyectos completados

### v1.2 — Funcionalidades avanzadas
- [ ] Guía de desmontaje para mudanzas y ventas de segunda mano
- [ ] Estimación de tiempo de montaje con IA
- [ ] Memoria entre sesiones — GIA recuerda proyectos anteriores
- [ ] Detección automática de tipo de proyecto desde la imagen

### v2.0 — Escalabilidad
- [ ] Google OAuth
- [ ] Plan Pro con límites ampliados
- [ ] OCR para manuales escaneados sin texto seleccionable
- [ ] API pública para integraciones con tiendas de muebles
- [ ] Procesamiento asíncrono con Celery (actualmente síncrono por limitaciones de Render Free)

---

## Decisiones de diseño

**¿Por qué Groq y no OpenAI?**
Groq ofrece inferencia ultrarrápida sobre modelos open-weight sin coste en el tier gratuito. Para un MVP con presupuesto cero, es la opción correcta.

**¿Por qué Anthropic para PDFs e imágenes?**
Claude Haiku es el modelo más barato del mercado para tareas de extracción y análisis de texto. La calidad de comprensión de manuales técnicos es superior a otros modelos pequeños y el límite de contexto (200k tokens) permite procesar manuales largos sin chunking agresivo.

**¿Por qué procesamiento síncrono?**
Render Free no soporta workers en background (Celery). Todo el procesamiento es síncrono con timeouts de 60 segundos. En producción real se migraría a procesamiento asíncrono con colas de trabajo.

**¿Por qué dos repos?**
Un repo público para el portfolio y la evaluación académica. Un repo privado para proteger la lógica de negocio, el sistema de prompts y la arquitectura de agentes.

---

## Autora

**Genesis Falcón **
Graduada de 4Geeks Academy, España.

---

*GIA nació de la frustración real de montar un mueble sin entender el manual. Está diseñado para ser útil de verdad, no solo para el portfolio.*
