# FOMO — Encuentra tu comunidad 🎯

> Plataforma digital para descubrir, comparar y unirse a actividades recreativas y comunidades en Santiago de Chile.

**🌐 Ver en vivo:** [https://bernimckay-crypto.github.io/FOMO-MVP-v2](https://bernimckay-crypto.github.io/FOMO-MVP-v2)

---

## ¿Qué es FOMO?

FOMO transforma el proceso fragmentado de buscar actividades por Instagram, WhatsApp y sitios web en una decisión simple, confiable y rápida desde un único canal.

### Para usuarios
- Descubrir talleres, deportes y comunidades filtrados por interés, nivel y zona
- Ver qué amigos y contactos ya participan en cada actividad
- Acumular puntos y canjearlos por clases gratis
- Recibir recomendaciones personalizadas con IA

### Para organizadores
- Publicar y gestionar actividades desde un dashboard propio
- Ver inscritos, pagos, cupos y lista de espera en tiempo real
- Métricas de visualizaciones, conversión y horarios más demandados

---

## Funcionalidades del MVP

### 🚀 Flujo de onboarding completo
- Pantalla de bienvenida con branding
- Selección de rol (Usuario / Organizador)
- Perfil personalizado en 5 pasos
- Pantalla de carga con recomendaciones personalizadas

### 👤 Vista Usuario
- **Catálogo** con 9 actividades de distintas categorías
- **Filtros dinámicos**: categoría, precio, modalidad, nivel, tipo
- **Recomendaciones IA** basadas en intereses del onboarding
- **Mapa interactivo** con pins por ubicación
- **Favoritos** guardados por sesión
- **Modal de actividad** completo: galería, beneficios, horarios, mapa, organizador, reseñas
- **Validación social**: contactos conocidos visibles en cada actividad
- **Inscripción** con formulario completo
- **Testimonios** con mensajería directa a usuarios
- **Chatbot Fomito** conectado a Claude API

### ⭐ Sistema de Puntos FOMO
| Acción | Puntos |
|--------|--------|
| Inscripción | +100 pts |
| Asistencia | +50 pts |
| Referido | +200 pts |
| Recomendación IA | +75 pts |
| Favorito | +10 pts |
| Reseña | +25 pts |

**Recompensas canjeables**: clase gratis, descuento 30%, acceso VIP, Kit FOMO y más.

### 👥 Conexiones Sociales y Validación
- Contactos conocidos visibles dentro de cada actividad
- Indicador "X amigos ya están inscritos" en tarjetas y modal
- Social proof en el formulario de inscripción
- Tracking completo para análisis de impacto

### 🏢 Panel Organizador
- Dashboard con KPIs: actividades, inscritos, ingresos, ocupación, rating
- Gestión de actividades: crear, editar, duplicar
- Lista de inscritos con datos de contacto y puntos otorgados
- Historial de pagos cobrados y pendientes
- Bandeja de mensajes y consultas
- Métricas: visualizaciones, conversión, horarios más demandados, lista de espera

### 🔐 Panel Administrador (oculto)
Acceso: `Ctrl + Shift + A` o ícono ⚙ en el footer

- **Overview**: 12 KPIs, categorías populares, ranking de organizadores
- **Funnel**: conversión por etapa con barras visuales
- **Leads**: tabla filtrable con búsqueda por nombre, email y canal
- **Actividades**: más visitadas, favoritos, inscripciones, CVR
- **🤖 Panel IA**: consultas, recomendaciones, inscripciones post-chat, CVR de IA
- **👥 Social Trust Analytics**: impacto de conexiones sociales en conversión
- **⭐ Puntos**: puntos emitidos, canjeados, historial
- **Eventos**: feed en tiempo real de todas las interacciones
- **Lista de espera**: emails capturados
- **Exportar**: CSV y Excel con datos reales

---

## Stack tecnológico

| Tecnología | Uso |
|------------|-----|
| HTML + CSS + JavaScript | Frontend (sin frameworks) |
| [Supabase](https://supabase.com) | Base de datos PostgreSQL + API REST |
| [Claude API](https://anthropic.com) | Chatbot de recomendaciones IA |
| GitHub Pages | Hosting gratuito |

---

## Base de datos (Supabase)

Las siguientes tablas deben existir en tu proyecto Supabase:

```sql
-- Ejecutar en Supabase → SQL Editor
create table public.usuarios (id uuid default gen_random_uuid() primary key, created_at timestamptz default now(), nombre text, email text unique, whatsapp text, edad text, zona text, intereses text[], nivel text, horarios text[], budget int, rol text default 'usuario');
create table public.organizadores (id uuid default gen_random_uuid() primary key, created_at timestamptz default now(), nombre text, org_nombre text, email text unique, whatsapp text, instagram text, categorias text[]);
create table public.inscripciones (id uuid default gen_random_uuid() primary key, created_at timestamptz default now(), nombre text, apellido text, email text, whatsapp text, edad text, canal text, actividad text, actividad_id int, estado text default 'pendiente', via_ia boolean default false, via_social boolean default false);
create table public.lista_espera (id uuid default gen_random_uuid() primary key, created_at timestamptz default now(), nombre text, email text, zona text);
create table public.eventos (id uuid default gen_random_uuid() primary key, created_at timestamptz default now(), tipo text, descripcion text, metadata jsonb);
create table public.favoritos (id uuid default gen_random_uuid() primary key, created_at timestamptz default now(), user_email text, actividad_id int, actividad_nombre text);

-- RLS policies
alter table public.usuarios enable row level security;
alter table public.organizadores enable row level security;
alter table public.inscripciones enable row level security;
alter table public.lista_espera enable row level security;
alter table public.eventos enable row level security;
alter table public.favoritos enable row level security;

create policy "allow_all" on public.usuarios for all using (true) with check (true);
create policy "allow_all" on public.organizadores for all using (true) with check (true);
create policy "allow_all" on public.inscripciones for all using (true) with check (true);
create policy "allow_all" on public.lista_espera for all using (true) with check (true);
create policy "allow_all" on public.eventos for all using (true) with check (true);
create policy "allow_all" on public.favoritos for all using (true) with check (true);
```

---

## Cómo publicar en GitHub Pages

1. Crear nuevo repositorio en GitHub
2. Subir los archivos de este repositorio
3. Ir a **Settings → Pages**
4. Seleccionar branch `main` → carpeta `/ (root)`
5. Guardar — el sitio estará disponible en `https://tuusuario.github.io/nombre-repo`

---

## Accesos

| Rol | Cómo ingresar |
|-----|--------------|
| Usuario | Pantalla de bienvenida → Comenzar → Busco actividades |
| Organizador | Pantalla de bienvenida → Comenzar → Soy organizador |
| Admin | `Ctrl + Shift + A` desde cualquier pantalla, o ⚙ en el footer |

---

## Hipótesis validadas con este MVP

- **H1**: Los usuarios prefieren descubrir actividades con validación social (amigos inscritos)
- **H2**: Las recomendaciones de IA aumentan la tasa de conversión
- **H3**: Un sistema de puntos aumenta la retención y recompra
- **H4**: La primera clase gratis reduce la barrera de entrada

---

## Equipo

Proyecto universitario — Santiago, Chile 2026
