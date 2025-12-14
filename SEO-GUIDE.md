# Guía de Optimización SEO - qaizn

## ✅ Optimizaciones Implementadas

### 1. Meta Tags Básicos
- **Title Tag**: Optimizado con palabras clave principales "IA para PyMEs", "Automatización", "Mejora Continua"
- **Meta Description**: 155 caracteres, incluye llamada a acción y valor diferencial
- **Meta Keywords**: Términos relevantes para el negocio
- **Canonical URL**: Previene contenido duplicado

### 2. Open Graph y Social Media
- **Open Graph Tags**: Para compartir en Facebook, LinkedIn
- **Twitter Cards**: Optimizado para Twitter
- **Imágenes sociales**: Referencias a og-image.jpg y twitter-image.jpg (necesitan crearse)

### 3. Structured Data (Schema.org)
- **Organization Schema**: Información estructurada del negocio
- **Service Schema**: Descripción de servicios ofrecidos
- Ayuda a Google a entender mejor el contenido

### 4. Accesibilidad (A11y)
- **Elementos semánticos HTML5**: `<header>`, `<main>`, `<footer>`, `<section>`
- **ARIA labels**: En navegación, botones y secciones
- **Alt text**: Atributos aria-label en SVGs
- **Roles**: role="img" en ilustraciones

### 5. Performance
- **Preconnect fonts**: Google Fonts con preconnect
- **SVG inline**: Logotipo e iconos en línea para carga rápida

### 6. Estructura Semántica
- **Jerarquía de headings**: H1 único, H2 para secciones, H3 para subsecciones
- **Footer informativo**: Copyright y descripción breve

---

## 📋 Tareas Pendientes para Completar SEO

### Imágenes de Redes Sociales
Crear estas imágenes en las dimensiones recomendadas:

1. **og-image.jpg** (1200x630px)
   - Para Facebook, LinkedIn
   - Debe incluir logo qaizn y mensaje clave
   - Texto grande y legible

2. **twitter-image.jpg** (1200x600px)
   - Similar a og-image pero ratio 2:1
   - Optimizada para Twitter

### robots.txt
Crear archivo `robots.txt` en la raíz:

```txt
User-agent: *
Allow: /

Sitemap: https://qaizn.com/sitemap.xml
```

### sitemap.xml
Crear sitemap XML para ayudar a Google a indexar:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
  <url>
    <loc>https://qaizn.com/</loc>
    <lastmod>2024-12-05</lastmod>
    <changefreq>weekly</changefreq>
    <priority>1.0</priority>
  </url>
</urlset>
```

### Google Analytics y Search Console
1. Añadir Google Analytics 4
2. Verificar propiedad en Google Search Console
3. Enviar sitemap a Search Console

### Performance Adicional
```html
<!-- Añadir al <head> -->
<link rel="preload" href="qaizn-logo.svg" as="image" type="image/svg+xml">
```

### Contenido Adicional para SEO
1. **Blog**: Crear sección de blog con artículos sobre:
   - "Cómo automatizar procesos con IA"
   - "Casos de éxito en PyMEs españolas"
   - "Guía para integrar IA en tu ERP"
   - Plantilla de artículo disponible en `/blog-posts/` para referencia

2. **FAQs**: Añadir sección de preguntas frecuentes con Schema.org FAQPage

3. **Testimonios**: Añadir testimonios de clientes con Schema.org Review

---

## 🎯 Palabras Clave Objetivo

### Primarias
- Inteligencia artificial PyMEs
- Automatización de procesos
- Consultoría IA España
- Mejora continua IA

### Secundarias
- Análisis predictivo ERP
- Optimización CRM con IA
- Transformación digital PyMEs
- Kaizen inteligencia artificial

### Long-tail
- "Cómo automatizar mi empresa con IA"
- "Consultor IA para pequeñas empresas"
- "Integrar inteligencia artificial en mi negocio"

---

## 📊 Métricas a Monitorizar

1. **Google Search Console**
   - Impresiones y clics
   - CTR (Click-through rate)
   - Posición promedio
   - Errores de indexación

2. **Google Analytics**
   - Páginas vistas
   - Tiempo en página
   - Tasa de rebote
   - Conversiones (formularios)

3. **Core Web Vitals**
   - LCP (Largest Contentful Paint) < 2.5s
   - FID (First Input Delay) < 100ms
   - CLS (Cumulative Layout Shift) < 0.1

---

## 🚀 Recomendaciones de Lanzamiento

1. ✅ **Antes del lanzamiento**
   - Crear imágenes OG
   - Configurar Google Analytics
   - Crear robots.txt y sitemap.xml
   - Comprimir y optimizar todas las imágenes
   - Probar en mobile y desktop

2. 📅 **Primera semana**
   - Verificar en Google Search Console
   - Enviar sitemap
   - Solicitar indexación manual
   - Compartir en redes sociales

3. 📈 **Primer mes**
   - Publicar 3-4 artículos de blog
   - Conseguir backlinks de calidad
   - Optimizar según analytics
   - A/B testing en CTAs

---

## 🔧 Herramientas Útiles

- **Google PageSpeed Insights**: https://pagespeed.web.dev/
- **Google Search Console**: https://search.google.com/search-console
- **Schema.org Validator**: https://validator.schema.org/
- **Open Graph Debugger**: https://www.opengraph.xyz/
- **Mobile-Friendly Test**: https://search.google.com/test/mobile-friendly

---

## ✨ Buenas Prácticas Implementadas

- ✅ Contenido único y relevante
- ✅ Estructura de URL limpia
- ✅ Headings jerárquicos correctos
- ✅ Imágenes con atributos descriptivos
- ✅ Enlaces internos coherentes
- ✅ Responsive design
- ✅ Velocidad de carga optimizada
- ✅ HTTPS (cuando se despliegue)
- ✅ Schema.org structured data
- ✅ Social media meta tags

---

**Última actualización**: 5 de diciembre de 2024
**Versión**: 1.0
