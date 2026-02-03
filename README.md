<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Creaciones Baugilù | Manualidades y Útiles</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Font Awesome -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- Google Fonts -->
    <link href="https://fonts.googleapis.com/css2?family=Fredoka:wght@300;400;600&family=Nunito:wght@400;600;700&display=swap" rel="stylesheet">
    <!-- Markdown Parser for AI responses -->
    <script src="https://cdn.jsdelivr.net/npm/marked/marked.min.js"></script>
    
    <script>
        /* --- CONFIGURACIÓN DE COLORES ---
           Aquí puedes cambiar los colores de la marca. 
           Usa códigos Hexadecimales (ej: #FF0000 es rojo).
        */
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        brand: {
                            pink: '#48CAE4',   /* Color Principal 1 (Azul Cielo) */
                            purple: '#0077B6', /* Color Principal 2 (Azul Océano) */
                            blue: '#0096C7',   /* Color Secundario */
                            yellow: '#E0F7FA', /* Color de Fondo Claro */
                            dark: '#023E8A'    /* Color de Texto Oscuro */
                        }
                    },
                    fontFamily: {
                        heading: ['Fredoka', 'sans-serif'],
                        body: ['Nunito', 'sans-serif'],
                    }
                }
            }
        }
    </script>
    <style>
        body { font-family: 'Nunito', sans-serif; }
        h1, h2, h3, h4, .font-heading { font-family: 'Fredoka', sans-serif; }
        .scroll-smooth { scroll-behavior: smooth; }
        @keyframes bounce-short {
            0%, 100% { transform: translateY(0); }
            50% { transform: translateY(-5px); }
        }
        .animate-bounce-short { animation: bounce-short 0.3s ease-in-out; }
        #toast {
            visibility: hidden;
            min-width: 250px;
            background-color: #333;
            color: #fff;
            text-align: center;
            border-radius: 8px;
            padding: 16px;
            position: fixed;
            z-index: 120;
            left: 50%;
            bottom: 30px;
            transform: translateX(-50%);
            opacity: 0;
            transition: opacity 0.3s, bottom 0.3s;
            box-shadow: 0 4px 6px rgba(0,0,0,0.1);
        }
        #toast.show { visibility: visible; opacity: 1; bottom: 50px; }
        .scrollbar-hide::-webkit-scrollbar { display: none; }
        .scrollbar-hide { -ms-overflow-style: none; scrollbar-width: none; }
        .payment-option:checked + label {
            border-color: #0077B6;
            background-color: #E0F7FA;
            color: #023E8A;
        }
        .payment-option:checked + label .check-icon { opacity: 1; }
        .file-input-wrapper {
            position: relative;
            overflow: hidden;
            display: inline-block;
        }
        .file-input-wrapper input[type=file] {
            font-size: 100px;
            position: absolute;
            left: 0;
            top: 0;
            opacity: 0;
            cursor: pointer;
        }
        .typing-dot { animation: typing 1.4s infinite ease-in-out both; }
        .typing-dot:nth-child(1) { animation-delay: -0.32s; }
        .typing-dot:nth-child(2) { animation-delay: -0.16s; }
        @keyframes typing {
            0%, 80%, 100% { transform: scale(0); }
            40% { transform: scale(1); }
        }
        .prose p { margin-bottom: 0.5em; }
        .prose ul { list-style-type: disc; padding-left: 1.2em; margin-bottom: 0.5em; }
        .prose strong { color: #0077B6; }
        .generated-image-container {
            position: relative;
            overflow: hidden;
            border-radius: 0.75rem;
            box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1);
        }
        .generated-image-container::after {
            content: '✨ Idea generada por IA';
            position: absolute;
            bottom: 8px;
            right: 8px;
            background: rgba(0, 0, 0, 0.6);
            color: white;
            font-size: 10px;
            padding: 2px 6px;
            border-radius: 4px;
            pointer-events: none;
        }
        .download-btn {
            position: absolute;
            top: 8px;
            right: 8px;
            background: white;
            color: #023E8A;
            width: 32px;
            height: 32px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            box-shadow: 0 2px 4px rgba(0,0,0,0.2);
            transition: transform 0.2s;
            z-index: 10;
        }
        .download-btn:hover { transform: scale(1.1); color: #0077B6; }
    </style>
</head>
<body class="bg-gray-50 text-brand-dark flex flex-col min-h-screen">

    <!-- Navbar -->
    <nav class="bg-white shadow-md sticky top-0 z-40">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="flex justify-between items-center h-20">
                <!-- Logo -->
                <div class="flex-shrink-0 flex items-center gap-2 cursor-pointer" onclick="window.scrollTo(0,0)">
                    <i class="fa-solid fa-paintbrush text-brand-purple text-3xl"></i>
                    <span class="font-heading font-bold text-2xl tracking-wide text-brand-dark">
                        <!-- CAMBIAR AQUI: Nombre de la tienda -->
                        Creaciones <span class="text-brand-pink">Baugilù</span>
                    </span>
                </div>

                <!-- Desktop Menu -->
                <div class="hidden md:flex space-x-8 items-center">
                    <a href="#inicio" class="text-gray-600 hover:text-brand-purple font-semibold transition">Inicio</a>
                    <a href="#catalogo" class="text-gray-600 hover:text-brand-purple font-semibold transition">Catálogo</a>
                    <a href="#servicios" class="text-gray-600 hover:text-brand-purple font-semibold transition">Servicios</a>
                    <a href="#contacto" class="text-gray-600 hover:text-brand-purple font-semibold transition">Contacto</a>
                    
                    <button onclick="toggleCart()" class="relative p-2 text-brand-dark hover:text-brand-blue transition group">
                        <i class="fa-solid fa-cart-shopping text-xl group-hover:scale-110 transition-transform"></i>
                        <span id="cart-count" class="absolute top-0 right-0 inline-flex items-center justify-center px-2 py-1 text-xs font-bold leading-none text-white transform translate-x-1/4 -translate-y-1/4 bg-brand-pink rounded-full">0</span>
                    </button>
                </div>

                <!-- Mobile Menu Button -->
                <div class="md:hidden flex items-center">
                     <button onclick="toggleCart()" class="mr-4 relative p-2 text-brand-dark">
                        <i class="fa-solid fa-cart-shopping text-xl"></i>
                        <span id="cart-count-mobile" class="absolute top-0 right-0 inline-flex items-center justify-center px-1.5 py-0.5 text-xs font-bold leading-none text-white transform translate-x-1/4 -translate-y-1/4 bg-brand-pink rounded-full">0</span>
                    </button>
                    <button onclick="toggleMobileMenu()" class="text-gray-600 hover:text-brand-purple focus:outline-none">
                        <i class="fa-solid fa-bars text-2xl"></i>
                    </button>
                </div>
            </div>
        </div>

        <!-- Mobile Menu Panel -->
        <div id="mobile-menu" class="hidden md:hidden bg-white border-t border-gray-100 shadow-lg absolute w-full z-40">
            <div class="px-2 pt-2 pb-3 space-y-1 sm:px-3">
                <a href="#inicio" onclick="toggleMobileMenu()" class="block px-3 py-2 rounded-md text-base font-medium text-gray-700 hover:text-brand-purple hover:bg-gray-50">Inicio</a>
                <a href="#catalogo" onclick="toggleMobileMenu()" class="block px-3 py-2 rounded-md text-base font-medium text-gray-700 hover:text-brand-purple hover:bg-gray-50">Catálogo</a>
                <a href="#servicios" onclick="toggleMobileMenu()" class="block px-3 py-2 rounded-md text-base font-medium text-gray-700 hover:text-brand-purple hover:bg-gray-50">Servicios</a>
                <a href="#contacto" onclick="toggleMobileMenu()" class="block px-3 py-2 rounded-md text-base font-medium text-gray-700 hover:text-brand-purple hover:bg-gray-50">Contacto</a>
            </div>
        </div>
    </nav>

    <!-- Hero Section -->
    <section id="inicio" class="relative bg-brand-yellow/20 overflow-hidden">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-16 md:py-24 flex flex-col-reverse md:flex-row items-center">
            <div class="w-full md:w-1/2 text-center md:text-left z-10">
                <h1 class="text-4xl md:text-6xl font-heading font-bold text-brand-dark mb-6 leading-tight">
                    Donde tu imaginación <br>
                    <span class="text-brand-purple">cobra vida</span>
                </h1>
                <p class="text-lg text-gray-600 mb-8 max-w-lg mx-auto md:mx-0">
                    Encuentra los útiles escolares más lindos, manualidades únicas y servicios personalizados para tus proyectos especiales.
                </p>
                <div class="flex flex-col sm:flex-row gap-4 justify-center md:justify-start">
                    <a href="#catalogo" class="px-8 py-3 bg-brand-purple text-white font-bold rounded-full shadow-lg hover:bg-brand-blue transition transform hover:-translate-y-1">
                        Ver Productos
                    </a>
                    <a href="#servicios" class="px-8 py-3 bg-white text-brand-purple border-2 border-brand-purple font-bold rounded-full hover:bg-brand-purple hover:text-white transition">
                        Nuestros Servicios
                    </a>
                </div>
            </div>
            <div class="w-full md:w-1/2 mb-10 md:mb-0 relative">
                <!-- Decorative Blob -->
                <div class="absolute top-1/2 left-1/2 transform -translate-x-1/2 -translate-y-1/2 w-[300px] h-[300px] md:w-[500px] md:h-[500px] bg-brand-pink/30 rounded-full blur-3xl -z-10"></div>
                <img src="https://images.unsplash.com/photo-1452860606245-08befc0ff44b?ixlib=rb-4.0.3&auto=format&fit=crop&w=800&q=80" alt="Mesa de manualidades" class="rounded-2xl shadow-2xl w-full object-cover h-64 md:h-96 transform md:rotate-3 hover:rotate-0 transition duration-500">
            </div>
        </div>
    </section>

    <!-- Categories / Filter Section -->
    <section id="catalogo" class="py-16 bg-white">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="text-center mb-12">
                <span class="text-brand-blue font-bold tracking-wider uppercase text-sm">Nuestra Tienda</span>
                <h2 class="text-3xl md:text-4xl font-heading font-bold text-brand-dark mt-2">Productos Destacados</h2>
            </div>

            <!-- Filter Buttons -->
            <div class="flex flex-wrap justify-center gap-4 mb-10">
                <button onclick="filterProducts('todos')" class="filter-btn active px-6 py-2 rounded-full border border-gray-200 hover:border-brand-purple hover:text-brand-purple transition focus:outline-none bg-brand-dark text-white shadow-md" data-category="todos">Todo</button>
                <button onclick="filterProducts('escolar')" class="filter-btn px-6 py-2 rounded-full border border-gray-200 text-gray-600 hover:border-brand-purple hover:text-brand-purple transition focus:outline-none" data-category="escolar">Útiles Escolares</button>
                <button onclick="filterProducts('manualidades')" class="filter-btn px-6 py-2 rounded-full border border-gray-200 text-gray-600 hover:border-brand-pink hover:text-brand-pink transition focus:outline-none" data-category="manualidades">Manualidades</button>
                <button onclick="filterProducts('regalos')" class="filter-btn px-6 py-2 rounded-full border border-gray-200 text-gray-600 hover:border-brand-blue hover:text-brand-blue transition focus:outline-none" data-category="regalos">Regalos</button>
            </div>

            <div id="product-grid" class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-8">
                <!-- Los productos se inyectan aquí con Javascript -->
            </div>
        </div>
    </section>

    <!-- Services Section -->
    <section id="servicios" class="py-16 bg-brand-blue/5">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="text-center mb-16">
                <h2 class="text-3xl md:text-4xl font-heading font-bold text-brand-dark">Servicios Especiales</h2>
                <p class="text-gray-600 mt-4 max-w-2xl mx-auto">Más que productos, ofrecemos experiencias y soluciones personalizadas para ti. Haz clic en cada servicio para saber más.</p>
            </div>

            <div class="grid md:grid-cols-3 gap-8">
                <!-- Service 1: Personalización -->
                <div onclick="openServicePage('personalizacion')" class="bg-white p-8 rounded-2xl shadow-lg hover:shadow-xl transition text-center group cursor-pointer border border-transparent hover:border-brand-pink transform hover:-translate-y-1">
                    <div class="w-16 h-16 bg-brand-pink/20 text-brand-pink rounded-full flex items-center justify-center mx-auto mb-6 group-hover:scale-110 transition">
                        <i class="fa-solid fa-wand-magic-sparkles text-2xl"></i>
                    </div>
                    <h3 class="text-xl font-bold mb-3 text-brand-dark">Papelería Creativa & Personalización</h3>
                    <p class="text-gray-600 mb-4 line-clamp-2">Lleva tus ideas a nuestras manos. Creamos papelería única para ti.</p>
                    <span class="text-brand-pink font-bold text-sm">Ver detalles <i class="fa-solid fa-arrow-right ml-1"></i></span>
                </div>

                <!-- Service 2: Talleres -->
                <div onclick="openServicePage('talleres')" class="bg-white p-8 rounded-2xl shadow-lg hover:shadow-xl transition text-center group cursor-pointer border border-transparent hover:border-brand-purple transform hover:-translate-y-1">
                    <div class="w-16 h-16 bg-brand-purple/20 text-brand-purple rounded-full flex items-center justify-center mx-auto mb-6 group-hover:scale-110 transition">
                        <i class="fa-solid fa-scissors text-2xl"></i>
                    </div>
                    <h3 class="text-xl font-bold mb-3 text-brand-dark">Talleres Creativos</h3>
                    <p class="text-gray-600 mb-4 line-clamp-2">Aprende corte en Cameo, diseño en Canva, tareas académicas y más.</p>
                    <span class="text-brand-purple font-bold text-sm">Ver detalles <i class="fa-solid fa-arrow-right ml-1"></i></span>
                </div>

                <!-- Service 3: Arreglos -->
                <div onclick="openServicePage('arreglos')" class="bg-white p-8 rounded-2xl shadow-lg hover:shadow-xl transition text-center group cursor-pointer border border-transparent hover:border-brand-blue transform hover:-translate-y-1">
                    <div class="w-16 h-16 bg-brand-yellow/50 text-brand-dark rounded-full flex items-center justify-center mx-auto mb-6 group-hover:scale-110 transition">
                        <i class="fa-solid fa-gift text-2xl"></i>
                    </div>
                    <h3 class="text-xl font-bold mb-3 text-brand-dark">Arreglos Sorpresa</h3>
                    <p class="text-gray-600 mb-4 line-clamp-2">Regalos perfectos para Cumpleaños, San Valentín, Navidad y Bautizos.</p>
                    <span class="text-brand-blue font-bold text-sm">Ver detalles <i class="fa-solid fa-arrow-right ml-1"></i></span>
                </div>
            </div>
        </div>
    </section>

    <!-- FULL PAGE SERVICE DETAIL VIEW -->
    <div id="service-page" class="fixed inset-0 z-[100] bg-white overflow-y-auto hidden">
        <!-- Sticky Navigation -->
        <nav class="sticky top-0 z-10 bg-white/80 backdrop-blur-md shadow-sm border-b border-gray-100">
            <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 h-20 flex items-center justify-between">
                <button onclick="closeServicePage()" class="flex items-center gap-2 text-gray-600 hover:text-brand-dark font-bold transition">
                    <div class="w-10 h-10 rounded-full bg-gray-100 flex items-center justify-center group-hover:bg-gray-200">
                        <i class="fa-solid fa-arrow-left"></i>
                    </div>
                    <span>Volver al Inicio</span>
                </button>
                <div class="font-heading font-bold text-xl text-brand-dark hidden sm:block">Creaciones Baugilù</div>
            </div>
        </nav>

        <!-- Service Content -->
        <div>
            <!-- Hero Image Header -->
            <div class="relative h-[40vh] md:h-[50vh] w-full bg-gray-200 overflow-hidden">
                <div class="absolute inset-0 bg-black/40 z-10"></div>
                <img id="service-hero-img" src="" class="w-full h-full object-cover" alt="Service Hero">
                <div class="absolute bottom-0 left-0 w-full z-20 p-6 md:p-12 bg-gradient-to-t from-black/80 to-transparent">
                    <div class="max-w-7xl mx-auto">
                        <span id="service-subtitle" class="text-brand-pink font-bold uppercase tracking-widest text-sm mb-2 block">Nuestros Servicios</span>
                        <h1 id="service-page-title" class="text-4xl md:text-6xl font-heading font-bold text-white leading-tight">Título del Servicio</h1>
                    </div>
                </div>
            </div>

            <!-- Content Container -->
            <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-12 md:py-20">
                <div class="grid md:grid-cols-3 gap-12">
                    <!-- Main Description & Features -->
                    <div class="md:col-span-2 space-y-12">
                        <div>
                            <h2 class="text-2xl font-bold text-brand-dark mb-6 border-l-4 border-brand-purple pl-4">¿De qué trata este servicio?</h2>
                            <div id="service-page-desc" class="text-lg text-gray-600 leading-relaxed space-y-4"></div>
                        </div>
                        <div>
                            <h2 class="text-2xl font-bold text-brand-dark mb-6">Galería de Trabajos</h2>
                            <div id="service-gallery-grid" class="grid grid-cols-1 sm:grid-cols-2 gap-4"></div>
                        </div>
                    </div>
                    <!-- Sidebar Info -->
                    <div class="space-y-8">
                        <div class="bg-brand-yellow/20 p-8 rounded-3xl border border-brand-yellow/30">
                            <h3 class="font-bold text-xl text-brand-dark mb-6 flex items-center gap-2">
                                <i class="fa-solid fa-list-check text-brand-purple"></i> Lo que ofrecemos
                            </h3>
                            <div id="service-features-list" class="space-y-4"></div>
                        </div>
                        <div class="bg-brand-dark text-white p-8 rounded-3xl text-center shadow-xl relative overflow-hidden group">
                            <div class="absolute top-0 right-0 w-32 h-32 bg-white/10 rounded-full -mr-16 -mt-16 group-hover:scale-150 transition duration-700"></div>
                            <i class="fa-regular fa-comments text-4xl mb-4 text-brand-pink"></i>
                            <h3 class="font-bold text-2xl mb-2">¿Te interesa?</h3>
                            <p class="text-white/80 mb-6 text-sm">Cotiza tu proyecto personalizado ahora mismo. ¡Hacemos realidad tus ideas!</p>
                            <a href="#contacto" onclick="closeServicePage()" class="inline-block w-full py-3 bg-white text-brand-dark font-bold rounded-xl hover:bg-brand-pink hover:text-white transition shadow-lg">
                                Contactar Ahora
                            </a>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <!-- Contact Section -->
    <section id="contacto" class="py-16 bg-white relative overflow-hidden">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="bg-brand-dark rounded-3xl overflow-hidden shadow-2xl flex flex-col md:flex-row">
                <!-- Info Side -->
                <div class="w-full md:w-5/12 bg-brand-purple p-10 md:p-12 text-white flex flex-col justify-between relative">
                    <div class="absolute top-0 right-0 -mr-10 -mt-10 w-40 h-40 bg-white/10 rounded-full blur-2xl"></div>
                    
                    <div>
                        <h3 class="text-3xl font-heading font-bold mb-6">Contáctanos</h3>
                        <p class="mb-8 text-purple-100">¿Tienes un pedido especial o una duda? Escríbenos y te responderemos a la brevedad.</p>
                        
                        <!-- CONFIGURACIÓN: DATOS DE CONTACTO -->
                        <div class="space-y-4">
                            <a href="https://wa.me/584142497952" target="_blank" class="flex items-center gap-4 hover:text-brand-pink transition group">
                                <i class="fa-brands fa-whatsapp text-2xl group-hover:scale-110 transition-transform"></i>
                                <!-- CAMBIAR AQUI: Tu teléfono visible -->
                                <span>+58 414-249-7952</span>
                            </a>
                            <div class="flex items-center gap-4">
                                <i class="fa-regular fa-envelope text-2xl"></i>
                                <!-- CAMBIAR AQUI: Tu correo visible -->
                                <span>creacionesbaugilu@gmail.com</span>
                            </div>
                            <div class="flex items-center gap-4">
                                <i class="fa-solid fa-location-dot text-2xl"></i>
                                <!-- CAMBIAR AQUI: Tu dirección -->
                                <span>Centro Comercial Las Rosas, Local 12</span>
                            </div>
                        </div>
                    </div>

                    <div class="mt-12">
                        <p class="text-sm font-semibold uppercase tracking-wider mb-4 opacity-70">Síguenos</p>
                        <!-- CONFIGURACIÓN: REDES SOCIALES -->
                        <div class="flex gap-4">
                            <!-- CAMBIAR AQUI: Tu enlace de Instagram -->
                            <a href="https://instagram.com/creaciones_baugilu?igsh=MXJtb3EwNjF4eTdmYw%3D%3D" target="_blank" class="w-10 h-10 bg-white/20 rounded-full flex items-center justify-center hover:bg-white hover:text-brand-purple transition"><i class="fa-brands fa-instagram"></i></a>
                            <!-- CAMBIAR AQUI: Tu enlace de Facebook -->
                            <a href="#" class="w-10 h-10 bg-white/20 rounded-full flex items-center justify-center hover:bg-white hover:text-brand-purple transition"><i class="fa-brands fa-facebook-f"></i></a>
                        </div>
                    </div>
                </div>

                <!-- Form Side -->
                <div class="w-full md:w-7/12 p-10 md:p-12 bg-white relative">
                    <div id="form-loading" class="absolute inset-0 bg-white/90 z-10 hidden flex-col items-center justify-center">
                        <i class="fa-solid fa-circle-notch fa-spin text-4xl text-brand-purple mb-4"></i>
                        <p class="font-bold text-gray-600">Enviando mensaje...</p>
                    </div>
                    <div id="form-success" class="absolute inset-0 bg-white z-10 hidden flex-col items-center justify-center text-center p-8">
                        <div class="w-20 h-20 bg-green-100 text-green-500 rounded-full flex items-center justify-center mb-6">
                            <i class="fa-solid fa-check text-4xl"></i>
                        </div>
                        <h3 class="text-2xl font-bold text-gray-800 mb-2">¡Mensaje Enviado!</h3>
                        <p class="text-gray-600 mb-8">Gracias por escribirnos. Te responderemos a la brevedad a tu correo.</p>
                        <button onclick="resetContactForm()" class="px-6 py-2 border-2 border-brand-purple text-brand-purple font-bold rounded-lg hover:bg-brand-purple hover:text-white transition">
                            Enviar otro mensaje
                        </button>
                    </div>

                    <form id="contact-form" onsubmit="handleContact(event)" class="space-y-6">
                        <div class="grid md:grid-cols-2 gap-6">
                            <div>
                                <label class="block text-sm font-medium text-gray-700 mb-2">Nombre</label>
                                <input type="text" name="name" required class="w-full px-4 py-3 rounded-lg bg-gray-50 border border-gray-200 focus:border-brand-purple focus:ring-2 focus:ring-brand-purple/20 outline-none transition" placeholder="Tu nombre">
                            </div>
                            <div>
                                <label class="block text-sm font-medium text-gray-700 mb-2">Email</label>
                                <input type="email" name="email" required class="w-full px-4 py-3 rounded-lg bg-gray-50 border border-gray-200 focus:border-brand-purple focus:ring-2 focus:ring-brand-purple/20 outline-none transition" placeholder="tu@email.com">
                            </div>
                        </div>
                        <div>
                            <label class="block text-sm font-medium text-gray-700 mb-2">Asunto</label>
                            <select name="subject" class="w-full px-4 py-3 rounded-lg bg-gray-50 border border-gray-200 focus:border-brand-purple focus:ring-2 focus:ring-brand-purple/20 outline-none transition">
                                <option>Información general</option>
                                <option>Pedido personalizado</option>
                                <option>Inscripción a talleres</option>
                            </select>
                        </div>
                        <div>
                            <label class="block text-sm font-medium text-gray-700 mb-2">Mensaje</label>
                            <textarea name="message" rows="4" required class="w-full px-4 py-3 rounded-lg bg-gray-50 border border-gray-200 focus:border-brand-purple focus:ring-2 focus:ring-brand-purple/20 outline-none transition" placeholder="Cuéntanos qué necesitas..."></textarea>
                        </div>
                        <button type="submit" class="w-full py-3 bg-brand-dark text-white font-bold rounded-lg hover:bg-gray-800 transition shadow-lg flex justify-center items-center gap-2">
                            <span>Enviar Mensaje</span>
                            <i class="fa-regular fa-paper-plane"></i>
                        </button>
                    </form>
                </div>
            </div>
        </div>
    </section>

    <!-- Footer -->
    <footer class="bg-gray-900 text-gray-400 py-12 mt-auto">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 flex flex-col md:flex-row justify-between items-center gap-6">
            <div class="text-center md:text-left">
                <span class="font-heading font-bold text-2xl text-white">
                    Creaciones <span class="text-brand-pink">Baugilù</span>
                </span>
                <p class="mt-2 text-sm">Haciendo el mundo más colorido, una manualidad a la vez.</p>
            </div>
            <div class="flex flex-col md:flex-row items-center gap-6 text-sm">
                <a href="#" class="hover:text-white transition">Política de Privacidad</a>
                <a href="#" class="hover:text-white transition">Términos de Servicio</a>
                 <button onclick="toggleAdminMode()" class="text-gray-500 hover:text-white transition flex items-center gap-2 cursor-pointer p-2">
                    <i class="fa-solid fa-lock text-xs"></i>
                    <span id="admin-btn-text">Acceso Admin</span>
                </button>
            </div>
            <div class="text-sm">
                &copy; 2024 Creaciones Baugilù. Todos los derechos reservados.
            </div>
        </div>
    </footer>

    <!-- Shopping Cart Modal (Overlay) -->
    <div id="cart-modal" class="fixed inset-0 z-50 hidden">
        <div class="absolute inset-0 bg-black/50 backdrop-blur-sm transition-opacity" onclick="toggleCart()"></div>
        <div class="absolute top-0 right-0 w-full md:w-[450px] h-full bg-white shadow-2xl transform transition-transform duration-300 flex flex-col">
            <div class="px-6 py-4 border-b border-gray-100 flex justify-between items-center bg-gray-50">
                <h2 class="text-xl font-heading font-bold text-brand-dark">Tu Carrito</h2>
                <button onclick="toggleCart()" class="text-gray-400 hover:text-red-500 transition">
                    <i class="fa-solid fa-xmark text-2xl"></i>
                </button>
            </div>
            <div id="cart-items-container" class="flex-1 overflow-y-auto p-6 space-y-4">
                <div id="cart-empty-state" class="h-full flex flex-col items-center justify-center text-gray-400 text-center">
                    <i class="fa-solid fa-basket-shopping text-6xl mb-4 text-gray-200"></i>
                    <p class="text-lg">Tu carrito está vacío</p>
                    <button onclick="toggleCart()" class="mt-4 text-brand-purple font-bold hover:underline">Ir al catálogo</button>
                </div>
            </div>
            <div class="p-6 border-t border-gray-100 bg-gray-50">
                <div class="flex justify-between items-center mb-4">
                    <span class="text-gray-600">Subtotal</span>
                    <span id="cart-subtotal" class="font-bold text-xl text-brand-dark">$0.00</span>
                </div>
                <button onclick="openPaymentModal()" class="w-full py-4 bg-brand-pink text-white font-bold rounded-xl shadow-lg hover:bg-brand-blue transition flex justify-center items-center gap-2">
                    Completar Pedido <i class="fa-solid fa-arrow-right"></i>
                </button>
            </div>
        </div>
    </div>

    <!-- Payment Selection Modal -->
    <div id="payment-modal" class="fixed inset-0 z-[60] hidden">
        <div class="absolute inset-0 bg-black/60 backdrop-blur-sm transition-opacity" onclick="closePaymentModal()"></div>
        <div class="absolute top-1/2 left-1/2 transform -translate-x-1/2 -translate-y-1/2 w-full max-w-md bg-white rounded-3xl shadow-2xl p-0 overflow-hidden">
            <div class="bg-brand-dark p-6 text-white text-center relative">
                 <button onclick="closePaymentModal()" class="absolute top-4 right-4 text-white/70 hover:text-white">
                    <i class="fa-solid fa-xmark text-xl"></i>
                </button>
                <h2 class="text-2xl font-heading font-bold">Finalizar Compra</h2>
                <p class="text-brand-pink text-sm mt-1">Selecciona tu método de pago</p>
                <div class="mt-4 flex justify-center gap-6 bg-white/10 rounded-xl py-3">
                    <div class="text-center">
                        <span class="block text-xs opacity-70">Total USD</span>
                        <span id="pay-total-usd" class="font-bold text-lg">$0.00</span>
                    </div>
                    <div class="w-px bg-white/20"></div>
                    <div class="text-center">
                        <span class="block text-xs opacity-70">Total Bs (aprox)</span>
                        <span id="pay-total-ves" class="font-bold text-lg">Bs 0.00</span>
                    </div>
                </div>
            </div>
            <div class="p-6">
                <form id="payment-form" onsubmit="finalizeOrder(event)">
                    <div class="space-y-3 mb-6">
                        <div class="relative">
                            <input type="radio" name="payment_method" id="method-ves" value="Pago Móvil" class="payment-option peer hidden" checked onchange="updatePaymentInfo()">
                            <label for="method-ves" class="flex items-center gap-4 p-4 border border-gray-200 rounded-xl cursor-pointer hover:bg-gray-50 transition border-l-4 border-l-transparent">
                                <div class="w-10 h-10 bg-gray-100 rounded-full flex items-center justify-center text-brand-dark">
                                    <i class="fa-solid fa-money-bill-transfer"></i>
                                </div>
                                <div class="flex-1">
                                    <h4 class="font-bold text-gray-800">Pago Móvil (Bs)</h4>
                                    <p class="text-xs text-gray-500">Transferencia bancaria nacional</p>
                                </div>
                                <i class="fa-solid fa-circle-check text-brand-purple text-xl opacity-0 check-icon transition"></i>
                            </label>
                        </div>
                        <div class="relative">
                            <input type="radio" name="payment_method" id="method-paypal" value="PayPal" class="payment-option peer hidden" onchange="updatePaymentInfo()">
                            <label for="method-paypal" class="flex items-center gap-4 p-4 border border-gray-200 rounded-xl cursor-pointer hover:bg-gray-50 transition border-l-4 border-l-transparent">
                                <div class="w-10 h-10 bg-blue-100 rounded-full flex items-center justify-center text-blue-600">
                                    <i class="fa-brands fa-paypal"></i>
                                </div>
                                <div class="flex-1">
                                    <h4 class="font-bold text-gray-800">PayPal ($)</h4>
                                    <p class="text-xs text-gray-500">Pagos internacionales</p>
                                </div>
                                <i class="fa-solid fa-circle-check text-brand-purple text-xl opacity-0 check-icon transition"></i>
                            </label>
                        </div>
                        <div class="relative">
                            <input type="radio" name="payment_method" id="method-card" value="Tarjeta" class="payment-option peer hidden" onchange="updatePaymentInfo()">
                            <label for="method-card" class="flex items-center gap-4 p-4 border border-gray-200 rounded-xl cursor-pointer hover:bg-gray-50 transition border-l-4 border-l-transparent">
                                <div class="w-10 h-10 bg-purple-100 rounded-full flex items-center justify-center text-purple-600">
                                    <i class="fa-regular fa-credit-card"></i>
                                </div>
                                <div class="flex-1">
                                    <h4 class="font-bold text-gray-800">Tarjeta de Crédito</h4>
                                    <p class="text-xs text-gray-500">Link de pago seguro</p>
                                </div>
                                <i class="fa-solid fa-circle-check text-brand-purple text-xl opacity-0 check-icon transition"></i>
                            </label>
                        </div>
                    </div>
                    <div id="payment-details" class="bg-gray-50 p-4 rounded-xl mb-6 text-sm border border-gray-100"></div>
                    <div class="mb-6">
                        <label class="block text-xs font-bold text-gray-500 uppercase mb-2">Referencia de Pago (Opcional)</label>
                        <input type="text" id="payment-ref" class="w-full px-4 py-3 rounded-lg border border-gray-300 focus:border-brand-purple focus:ring-2 focus:ring-brand-purple/20 outline-none text-sm" placeholder="Ej: 12345678 o Email de PayPal">
                    </div>
                    <button type="submit" class="w-full py-4 bg-green-500 hover:bg-green-600 text-white font-bold rounded-xl shadow-lg transition flex justify-center items-center gap-2">
                        <i class="fa-brands fa-whatsapp text-xl"></i> Enviar Pedido a WhatsApp
                    </button>
                </form>
            </div>
        </div>
    </div>
    
    <!-- Product Details Modal -->
    <div id="product-details-modal" class="fixed inset-0 z-[80] hidden bg-white overflow-y-auto">
        <div class="sticky top-0 bg-white shadow-sm z-10 px-4 py-3 flex justify-between items-center max-w-7xl mx-auto w-full">
            <button onclick="closeProductDetails()" class="flex items-center gap-2 text-gray-600 hover:text-brand-purple transition">
                <i class="fa-solid fa-arrow-left text-xl"></i> <span class="hidden sm:inline">Volver</span>
            </button>
            <div class="flex gap-4">
                 <button onclick="toggleCart()" class="relative text-brand-dark p-2">
                    <i class="fa-solid fa-cart-shopping text-xl"></i>
                    <span id="details-cart-count" class="absolute top-0 right-0 -mt-1 -mr-1 bg-brand-pink text-white text-xs font-bold px-1.5 py-0.5 rounded-full">0</span>
                </button>
            </div>
        </div>
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-8">
            <div class="grid grid-cols-1 md:grid-cols-2 gap-8 lg:gap-12">
                <div class="space-y-4">
                    <div class="aspect-square bg-gray-100 rounded-2xl overflow-hidden relative group shadow-sm border border-gray-100">
                        <img id="detail-main-image" src="" class="w-full h-full object-cover">
                    </div>
                    <div id="detail-gallery" class="flex gap-3 overflow-x-auto pb-2 scrollbar-hide"></div>
                </div>
                <div class="flex flex-col">
                    <span id="detail-category" class="text-brand-purple font-bold text-sm uppercase tracking-wider mb-2">Categoría</span>
                    <h1 id="detail-title" class="text-3xl md:text-4xl font-heading font-bold text-gray-900 mb-4 leading-tight">Nombre del Producto</h1>
                    <div class="flex items-end gap-3 mb-6 bg-gray-50 p-4 rounded-xl border border-gray-100 inline-flex">
                        <span id="detail-price" class="text-4xl font-bold text-brand-dark">$0.00</span>
                        <div class="flex flex-col">
                            <span class="text-gray-400 line-through text-sm" id="detail-price-old">$0.00</span> 
                            <span class="text-brand-pink font-bold text-xs">-20% Desc.</span>
                        </div>
                    </div>
                    <div class="bg-blue-50/50 p-4 rounded-xl border border-blue-100 mb-6 space-y-3 text-sm">
                        <div class="flex items-center gap-3 text-green-600 font-medium"><i class="fa-solid fa-check-circle"></i> <span>Disponible en Stock</span></div>
                        <div class="flex items-center gap-3 text-gray-600"><i class="fa-solid fa-truck-fast text-brand-purple"></i> <span>Envío a todo el país (Cobro en destino)</span></div>
                        <div class="flex items-center gap-3 text-gray-600"><i class="fa-solid fa-shield-heart text-brand-pink"></i> <span>Garantía de satisfacción Baugilù</span></div>
                    </div>
                    <div class="mb-8">
                        <h3 class="font-bold text-gray-900 mb-2 border-b border-gray-100 pb-2">Características del producto:</h3>
                        <p id="detail-desc" class="text-gray-600 leading-relaxed text-base">Descripción del producto...</p>
                    </div>
                    <div class="mt-auto pt-6">
                        <div class="flex items-center gap-4 mb-6">
                            <span class="font-bold text-gray-700">Cantidad:</span>
                            <div class="flex items-center border border-gray-300 rounded-lg bg-white">
                                <button onclick="adjustDetailQty(-1)" class="px-4 py-2 text-gray-600 hover:bg-gray-100 rounded-l-lg">-</button>
                                <input type="number" id="detail-qty" value="1" class="w-12 text-center border-none outline-none font-bold text-brand-dark" readonly>
                                <button onclick="adjustDetailQty(1)" class="px-4 py-2 text-gray-600 hover:bg-gray-100 rounded-r-lg">+</button>
                            </div>
                            <span class="text-xs text-gray-400 ml-2">(Unidades disponibles)</span>
                        </div>
                        <div class="flex flex-col sm:flex-row gap-4">
                            <button onclick="addToCartFromDetail()" class="flex-1 bg-brand-pink/10 text-brand-pink border-2 border-brand-pink font-bold py-4 rounded-xl hover:bg-brand-pink hover:text-white transition flex items-center justify-center gap-2">
                                <i class="fa-solid fa-cart-plus"></i> Agregar al Carrito
                            </button>
                            <button onclick="buyNowFromDetail()" class="flex-1 bg-brand-dark text-white font-bold py-4 rounded-xl shadow-lg hover:bg-brand-purple transition flex items-center justify-center gap-2 transform hover:scale-[1.02]">
                                <i class="fa-solid fa-bag-shopping"></i> Comprar Ahora
                            </button>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <!-- Add Product Floating Button -->
    <button id="add-product-btn" onclick="openAddProductModal()" class="fixed bottom-6 right-6 w-14 h-14 bg-brand-pink text-white rounded-full shadow-2xl flex items-center justify-center hover:bg-brand-blue transition transform hover:scale-110 z-30 group hidden" title="Agregar Producto">
        <i class="fa-solid fa-plus text-2xl group-hover:rotate-90 transition duration-300"></i>
    </button>

    <!-- AI Assistant Floating Button -->
    <button onclick="toggleAIChat()" class="fixed bottom-6 left-6 w-14 h-14 bg-gradient-to-r from-brand-purple to-brand-blue text-white rounded-full shadow-2xl flex items-center justify-center hover:scale-110 transition z-30 group" title="Asistente Baugilù">
        <i class="fa-solid fa-wand-magic-sparkles text-2xl group-hover:animate-pulse"></i>
        <span class="absolute top-0 right-0 -mt-1 -mr-1 flex h-4 w-4">
            <span class="animate-ping absolute inline-flex h-full w-full rounded-full bg-brand-pink opacity-75"></span>
            <span class="relative inline-flex rounded-full h-4 w-4 bg-brand-pink"></span>
        </span>
    </button>

    <!-- AI Chat Modal -->
    <div id="ai-chat-modal" class="fixed bottom-24 left-6 w-[90%] max-w-[350px] md:w-[400px] h-[500px] bg-white rounded-2xl shadow-2xl z-[60] flex flex-col hidden border border-gray-100 overflow-hidden transform transition-all duration-300 origin-bottom-left">
        <div class="bg-gradient-to-r from-brand-purple to-brand-blue p-4 text-white flex justify-between items-center shadow-md">
            <div class="flex items-center gap-3">
                <div class="w-10 h-10 bg-white/20 rounded-full flex items-center justify-center backdrop-blur-sm">
                    <i class="fa-solid fa-robot text-xl"></i>
                </div>
                <div>
                    <h3 class="font-bold text-lg leading-tight">Asistente Baugilù ✨</h3>
                    <p class="text-xs text-white/80 flex items-center gap-1"><span class="w-2 h-2 bg-green-400 rounded-full inline-block"></span> En línea</p>
                </div>
            </div>
            <button onclick="toggleAIChat()" class="text-white/80 hover:text-white transition">
                <i class="fa-solid fa-chevron-down"></i>
            </button>
        </div>
        <div id="ai-chat-messages" class="flex-1 overflow-y-auto p-4 space-y-4 bg-gray-50 scroll-smooth">
            <div class="flex items-start gap-2">
                <div class="w-8 h-8 bg-brand-purple rounded-full flex items-center justify-center text-white flex-shrink-0 text-xs">
                    <i class="fa-solid fa-wand-magic-sparkles"></i>
                </div>
                <div class="bg-white p-3 rounded-2xl rounded-tl-none shadow-sm text-sm text-gray-700 border border-gray-100">
                    ¡Hola! Soy tu asistente creativo virtual ✨. <br><br>
                    Puedo ayudarte a:<br>
                    🎁 Encontrar el regalo ideal en nuestro catálogo.<br>
                    📝 Escribir una dedicatoria bonita.<br>
                    📸 Visualizar una idea de arreglo o manualidad.
                </div>
            </div>
            <div class="flex gap-2 flex-wrap" id="ai-suggestions">
                <button onclick="sendQuickPrompt('Dame ideas de regalo para San Valentín')" class="text-xs bg-brand-pink/10 text-brand-dark px-3 py-1.5 rounded-full hover:bg-brand-pink hover:text-white transition border border-brand-pink/20">🎁 Regalo San Valentín</button>
                <button onclick="sendQuickPrompt('Quiero ver ideas de ramos de rosas')" class="text-xs bg-brand-purple/10 text-brand-dark px-3 py-1.5 rounded-full hover:bg-brand-purple hover:text-white transition border border-brand-purple/20">🌹 Ver Ramos</button>
                <button onclick="sendQuickPrompt('¿Qué tienes por menos de $20?')" class="text-xs bg-brand-blue/10 text-brand-dark px-3 py-1.5 rounded-full hover:bg-brand-blue hover:text-white transition border border-brand-blue/20">💰 Ofertas</button>
            </div>
        </div>
        <div class="p-3 bg-white border-t border-gray-100">
            <form onsubmit="handleAIChat(event)" class="relative flex items-center gap-2">
                <input type="text" id="ai-user-input" class="w-full pl-4 pr-12 py-3 rounded-full bg-gray-100 focus:bg-white border border-transparent focus:border-brand-purple focus:ring-0 text-sm transition outline-none" placeholder="Escribe tu pregunta aquí...">
                <button type="submit" id="ai-send-btn" class="absolute right-2 w-8 h-8 bg-brand-purple text-white rounded-full flex items-center justify-center hover:bg-brand-dark transition shadow-sm">
                    <i class="fa-solid fa-paper-plane text-xs"></i>
                </button>
            </form>
        </div>
    </div>

    <!-- Add Product Modal -->
    <div id="add-product-modal" class="fixed inset-0 z-[70] hidden">
        <div class="absolute inset-0 bg-black/60 backdrop-blur-sm transition-opacity" onclick="closeAddProductModal()"></div>
        <div class="absolute top-1/2 left-1/2 transform -translate-x-1/2 -translate-y-1/2 w-full max-w-lg bg-white rounded-2xl shadow-2xl p-0 overflow-hidden max-h-[90vh] overflow-y-auto">
            <div class="bg-brand-dark p-6 text-white flex justify-between items-center">
                <h3 class="text-xl font-heading font-bold">Agregar Nuevo Producto</h3>
                <button onclick="closeAddProductModal()" class="text-white/70 hover:text-white"><i class="fa-solid fa-xmark text-xl"></i></button>
            </div>
            <div class="p-6">
                <form id="add-product-form" onsubmit="handleNewProduct(event)" class="space-y-4">
                    <div>
                        <label class="block text-sm font-bold text-gray-700 mb-1">Nombre del Producto</label>
                        <input type="text" id="add-name" name="name" required class="w-full px-4 py-2 rounded-lg border border-gray-300 focus:border-brand-pink outline-none" placeholder="Ej: Set de Lápices Neon">
                    </div>
                    <div class="grid grid-cols-2 gap-4">
                        <div>
                            <label class="block text-sm font-bold text-gray-700 mb-1">Categoría</label>
                            <select name="category" id="add-category" class="w-full px-4 py-2 rounded-lg border border-gray-300 focus:border-brand-pink outline-none">
                                <option value="escolar">Útiles Escolares</option>
                                <option value="manualidades">Manualidades</option>
                                <option value="regalos">Regalos</option>
                            </select>
                        </div>
                        <div>
                            <label class="block text-sm font-bold text-gray-700 mb-1">Precio ($)</label>
                            <input type="number" name="price" step="0.01" required class="w-full px-4 py-2 rounded-lg border border-gray-300 focus:border-brand-pink outline-none" placeholder="0.00">
                        </div>
                    </div>
                    <div>
                        <div class="flex justify-between items-center mb-1">
                            <label class="block text-sm font-bold text-gray-700">Descripción</label>
                            <button type="button" onclick="generateDescription('add-name', 'add-category', 'add-desc')" class="text-xs bg-brand-purple/10 text-brand-purple px-2 py-1 rounded-full hover:bg-brand-purple hover:text-white transition flex items-center gap-1">
                                <i class="fa-solid fa-wand-magic-sparkles"></i> <span>✨ Crear con IA</span>
                            </button>
                        </div>
                        <textarea name="desc" id="add-desc" rows="3" required class="w-full px-4 py-2 rounded-lg border border-gray-300 focus:border-brand-pink outline-none" placeholder="Detalles del producto..."></textarea>
                    </div>
                    <div class="border-t border-gray-100 pt-4 mt-2">
                        <label class="block text-sm font-bold text-brand-purple mb-2"><i class="fa-solid fa-images mr-1"></i> Galería de Imágenes</label>
                        <div class="space-y-4">
                             <div>
                                <label class="block text-xs text-gray-500 mb-2">Imagen Principal (Desde tu dispositivo)</label>
                                <div class="flex items-center gap-3">
                                    <label class="file-input-wrapper w-full bg-gray-100 hover:bg-gray-200 text-gray-600 font-bold py-2 px-4 rounded-lg border border-gray-300 cursor-pointer text-center transition flex items-center justify-center gap-2">
                                        <i class="fa-solid fa-upload"></i> <span>Seleccionar Archivo</span>
                                        <input type="file" id="add-image-file" accept="image/*" onchange="previewImage(this, 'add-image-preview')">
                                    </label>
                                </div>
                                <img id="add-image-preview" class="h-24 w-full object-contain mt-3 rounded-lg border border-gray-200 hidden bg-gray-50">
                            </div>
                            <div>
                                <label class="block text-xs text-gray-500 mb-2">Fotos Adicionales (Opcional - Selección múltiple)</label>
                                <label class="file-input-wrapper w-full bg-gray-100 hover:bg-gray-200 text-gray-600 font-bold py-2 px-4 rounded-lg border border-gray-300 cursor-pointer text-center transition flex items-center justify-center gap-2">
                                    <i class="fa-solid fa-images"></i> <span>Seleccionar Galería</span>
                                    <input type="file" id="add-gallery-files" accept="image/*" multiple onchange="previewGallery(this, 'add-gallery-preview')">
                                </label>
                                <div id="add-gallery-preview" class="flex gap-2 mt-3 overflow-x-auto pb-2"></div>
                            </div>
                        </div>
                    </div>
                    <button type="submit" class="w-full py-3 bg-brand-pink text-white font-bold rounded-lg hover:bg-brand-blue transition shadow-md mt-4">
                        <i class="fa-solid fa-save mr-2"></i> Guardar Producto
                    </button>
                </form>
            </div>
        </div>
    </div>

    <!-- Edit Product Modal -->
    <div id="edit-product-modal" class="fixed inset-0 z-[75] hidden">
        <div class="absolute inset-0 bg-black/60 backdrop-blur-sm transition-opacity" onclick="closeEditProductModal()"></div>
        <div class="absolute top-1/2 left-1/2 transform -translate-x-1/2 -translate-y-1/2 w-full max-w-lg bg-white rounded-2xl shadow-2xl p-0 overflow-hidden max-h-[90vh] overflow-y-auto">
            <div class="bg-brand-purple p-6 text-white flex justify-between items-center">
                <h3 class="text-xl font-heading font-bold">Editar Producto</h3>
                <button onclick="closeEditProductModal()" class="text-white/70 hover:text-white"><i class="fa-solid fa-xmark text-xl"></i></button>
            </div>
            <div class="p-6">
                <form id="edit-product-form" onsubmit="handleUpdateProduct(event)" class="space-y-4">
                    <input type="hidden" name="id" id="edit-id">
                    <div>
                        <label class="block text-sm font-bold text-gray-700 mb-1">Nombre del Producto</label>
                        <input type="text" name="name" id="edit-name" required class="w-full px-4 py-2 rounded-lg border border-gray-300 focus:border-brand-purple outline-none">
                    </div>
                    <div class="grid grid-cols-2 gap-4">
                        <div>
                            <label class="block text-sm font-bold text-gray-700 mb-1">Categoría</label>
                            <select name="category" id="edit-category" class="w-full px-4 py-2 rounded-lg border border-gray-300 focus:border-brand-purple outline-none">
                                <option value="escolar">Útiles Escolares</option>
                                <option value="manualidades">Manualidades</option>
                                <option value="regalos">Regalos</option>
                            </select>
                        </div>
                        <div>
                            <label class="block text-sm font-bold text-gray-700 mb-1">Precio ($)</label>
                            <input type="number" name="price" id="edit-price" step="0.01" required class="w-full px-4 py-2 rounded-lg border border-gray-300 focus:border-brand-purple outline-none">
                        </div>
                    </div>
                    <div>
                        <div class="flex justify-between items-center mb-1">
                            <label class="block text-sm font-bold text-gray-700">Descripción</label>
                            <button type="button" onclick="generateDescription('edit-name', 'edit-category', 'edit-desc')" class="text-xs bg-brand-purple/10 text-brand-purple px-2 py-1 rounded-full hover:bg-brand-purple hover:text-white transition flex items-center gap-1">
                                <i class="fa-solid fa-wand-magic-sparkles"></i> <span>✨ Crear con IA</span>
                            </button>
                        </div>
                        <textarea name="desc" id="edit-desc" rows="3" required class="w-full px-4 py-2 rounded-lg border border-gray-300 focus:border-brand-purple outline-none"></textarea>
                    </div>
                    <div class="border-t border-gray-100 pt-4 mt-2">
                        <label class="block text-sm font-bold text-brand-purple mb-2"><i class="fa-solid fa-images mr-1"></i> Actualizar Imágenes</label>
                        <div class="space-y-4">
                             <div>
                                <label class="block text-xs text-gray-500 mb-2">Nueva Imagen Principal (Opcional)</label>
                                <label class="file-input-wrapper w-full bg-gray-100 hover:bg-gray-200 text-gray-600 font-bold py-2 px-4 rounded-lg border border-gray-300 cursor-pointer text-center transition flex items-center justify-center gap-2">
                                    <i class="fa-solid fa-upload"></i> <span>Cambiar Archivo</span>
                                    <input type="file" id="edit-image-file" accept="image/*" onchange="previewImage(this, 'edit-image-preview')">
                                </label>
                                <img id="edit-image-preview" class="h-24 w-full object-contain mt-3 rounded-lg border border-gray-200 bg-gray-50">
                            </div>
                            <div>
                                <label class="block text-xs text-gray-500 mb-2">Reemplazar Galería (Opcional)</label>
                                <label class="file-input-wrapper w-full bg-gray-100 hover:bg-gray-200 text-gray-600 font-bold py-2 px-4 rounded-lg border border-gray-300 cursor-pointer text-center transition flex items-center justify-center gap-2">
                                    <i class="fa-solid fa-images"></i> <span>Seleccionar Nuevas Fotos</span>
                                    <input type="file" id="edit-gallery-files" accept="image/*" multiple onchange="previewGallery(this, 'edit-gallery-preview')">
                                </label>
                                <div id="edit-gallery-preview" class="flex gap-2 mt-3 overflow-x-auto pb-2"></div>
                            </div>
                        </div>
                    </div>
                    <button type="submit" class="w-full py-3 bg-brand-purple text-white font-bold rounded-lg hover:bg-brand-dark transition shadow-md mt-4">
                        <i class="fa-solid fa-save mr-2"></i> Actualizar Producto
                    </button>
                </form>
            </div>
        </div>
    </div>

    <!-- Admin Login Modal -->
    <div id="admin-login-modal" class="fixed inset-0 z-[100] hidden">
        <div class="absolute inset-0 bg-black/60 backdrop-blur-sm transition-opacity" onclick="closeAdminLogin()"></div>
        <div class="absolute top-1/2 left-1/2 transform -translate-x-1/2 -translate-y-1/2 w-full max-w-sm bg-white rounded-2xl shadow-2xl p-6">
            <div class="text-center mb-6">
                <div class="w-12 h-12 bg-brand-dark text-white rounded-full flex items-center justify-center mx-auto mb-3">
                    <i class="fa-solid fa-user-shield text-xl"></i>
                </div>
                <h3 class="text-xl font-heading font-bold text-gray-800">Acceso Administrador</h3>
                <p class="text-sm text-gray-500">Ingresa la contraseña para gestionar la tienda.</p>
            </div>
            
            <form onsubmit="checkAdminLogin(event)">
                <div class="mb-4">
                    <input type="password" id="admin-pass-input" class="w-full px-4 py-3 rounded-lg border border-gray-300 focus:border-brand-dark outline-none text-center" placeholder="Contraseña" required>
                </div>
                <div class="flex gap-3">
                    <button type="button" onclick="closeAdminLogin()" class="flex-1 py-2 text-gray-500 hover:bg-gray-100 rounded-lg transition">Cancelar</button>
                    <button type="submit" class="flex-1 py-2 bg-brand-dark text-white font-bold rounded-lg hover:bg-brand-purple transition">Entrar</button>
                </div>
            </form>
        </div>
    </div>

    <!-- Toast Notification -->
    <div id="toast">Producto agregado al carrito</div>

    <script>
        // --- CONFIGURACIÓN: API KEY Y DATOS ---
        const exchangeRate = 45.00; // Tasa de cambio Bs/$
        
        // **IMPORTANTE**: Pega aquí tu API Key de Google AI Studio para activar el asistente
        const apiKey = "AIzaSyC3R8nFa1RMwN83nDSS2CV6vpguCIfhqDo"; 
        
        let currentDetailId = null;
        let isAdmin = false; // Estado del modo administrador
        
        // --- Service Details Data ---
        const serviceData = {
            'personalizacion': {
                title: 'Personalización y Papelería Creativa',
                heroImage: "https://images.unsplash.com/photo-1542435503-956c469947f6?ixlib=rb-4.0.3&auto=format&fit=crop&w=1600&q=80",
                description: `
                    <p>En <strong>Creaciones Baugilù</strong>, transformamos tus ideas en realidad tangible. Entendemos que cada detalle cuenta y que la papelería creativa es el alma de cualquier evento o regalo especial. Nuestro compromiso es llevar tus conceptos a nuestras manos y crear piezas únicas que reflejen exactamente lo que imaginas.</p>
                    <p>No somos solo una tienda, somos tus servidores creativos. Nos encargamos de todo el proceso de diseño, corte y armado para que tú solo tengas que disfrutar del resultado final.</p>
                `,
                features: [
                    'Cuadernos y Agendas Personalizadas con tu nombre o logo.',
                    'Etiquetas Escolares resistentes al agua.',
                    'Toppers para Tortas y Cupcakes temáticos.',
                    'Cajas y Empaques creativos para regalos.',
                    'Tarjetería fina para eventos sociales.'
                ],
                gallery: [
                    "https://images.unsplash.com/photo-1512413316925-fd4b93f31521?ixlib=rb-4.0.3&auto=format&fit=crop&w=600&q=80",
                    "https://images.unsplash.com/photo-1605117882932-f9e32b03ef3c?ixlib=rb-4.0.3&auto=format&fit=crop&w=600&q=80",
                    "https://images.unsplash.com/photo-1513542789411-b6a5d4f31634?ixlib=rb-4.0.3&auto=format&fit=crop&w=600&q=80",
                    "https://images.unsplash.com/photo-1586075010923-2dd4570fb338?ixlib=rb-4.0.3&auto=format&fit=crop&w=600&q=80"
                ]
            },
            'talleres': {
                title: 'Talleres Creativos y Academia',
                heroImage: "https://images.unsplash.com/photo-1626785774573-4b7993143c26?ixlib=rb-4.0.3&auto=format&fit=crop&w=1600&q=80",
                description: `
                    <p>Nuestra pasión no solo es crear, sino también enseñar. La <strong>Academia Baugilù</strong> nace para empoderar a emprendedores, estudiantes y creativos. Te brindamos las herramientas técnicas y prácticas para que domines el arte del diseño y las manualidades.</p>
                    <p>Ya sea que quieras iniciar tu propio negocio de papelería, necesites ayuda experta con tus tareas académicas o quieras mejorar la imagen de tu marca, tenemos un espacio para ti.</p>
                `,
                features: [
                    '<strong>Corte en Cameo:</strong> Domina el plotter de corte para vinil, cartulina y acetato.',
                    '<strong>Diseño en Canva:</strong> Aprende a crear posts, historias y material gráfico profesional.',
                    '<strong>Tareas Académicas:</strong> Asesoría y realización de maquetas y láminas escolares.',
                    '<strong>Creación de Logotipos:</strong> Diseño de identidad visual para nuevos emprendimientos.'
                ],
                gallery: [
                    "https://images.unsplash.com/photo-1572044162444-ad60f128bdea?ixlib=rb-4.0.3&auto=format&fit=crop&w=600&q=80",
                    "https://images.unsplash.com/photo-1516321318423-f06f85e504b3?ixlib=rb-4.0.3&auto=format&fit=crop&w=600&q=80",
                    "https://images.unsplash.com/photo-1501504905252-473c47e087f8?ixlib=rb-4.0.3&auto=format&fit=crop&w=600&q=80",
                    "https://images.unsplash.com/photo-1611162617474-5b21e879e113?ixlib=rb-4.0.3&auto=format&fit=crop&w=600&q=80"
                ]
            },
            'arreglos': {
                title: 'Arreglos Sorpresa para Toda Ocasión',
                heroImage: "https://images.unsplash.com/photo-1513201099705-a9746e1e201f?ixlib=rb-4.0.3&auto=format&fit=crop&w=1600&q=80",
                description: `
                    <p>Celebramos la vida contigo. Nuestros arreglos sorpresa están diseñados para emocionar y crear recuerdos inolvidables. Cada arreglo es una obra de arte personalizada según los gustos de esa persona especial.</p>
                    <p>Cubrimos todas las festividades del año y momentos personales importantes. No importa la ocasión, tenemos el detalle perfecto listo para ser entregado.</p>
                `,
                features: [
                    '<strong>Cumpleaños:</strong> Cajas sorpresa, desayunos y globos personalizados.',
                    '<strong>San Valentín:</strong> Arreglos románticos con chocolates y flores.',
                    '<strong>Navidad:</strong> Detalles corporativos y familiares.',
                    '<strong>Halloween:</strong> Dulceros temáticos y decoraciones espeluznantes.',
                    '<strong>Bautizos y Baby Showers:</strong> Recuerdos delicados y únicos.'
                ],
                gallery: [
                    "https://images.unsplash.com/photo-1549465220-1a8b9238cd48?ixlib=rb-4.0.3&auto=format&fit=crop&w=600&q=80",
                    "https://images.unsplash.com/photo-1518199266791-5375a83190b7?ixlib=rb-4.0.3&auto=format&fit=crop&w=600&q=80",
                    "https://images.unsplash.com/photo-1512909006721-3d6018887383?ixlib=rb-4.0.3&auto=format&fit=crop&w=600&q=80",
                    "https://images.unsplash.com/photo-1509557965875-b88c97052f0e?ixlib=rb-4.0.3&auto=format&fit=crop&w=600&q=80"
                ]
            }
        };
        
        const pagoMovilData = {
            banco: "Banco de Venezuela (0102)",
            telefono: "0412-123-4567",
            cedula: "V-12.345.678"
        };
        
        const paypalEmail = "creacionesbaugilu@gmail.com";

        // CAMBIAR AQUI: Lista de productos iniciales
        const defaultProducts = [
            {
                id: 1,
                name: "Set Escolar Kawaii",
                category: "escolar",
                price: 15.00,
                image: "https://images.unsplash.com/photo-1503926359680-90981268ca19?ixlib=rb-4.0.3&auto=format&fit=crop&w=600&q=80",
                desc: "Incluye lápices, borrador y notas adhesivas. Todo con diseños de gatitos y colores pastel. Ideal para el regreso a clases con estilo.",
                gallery: [
                    "https://images.unsplash.com/photo-1503926359680-90981268ca19?ixlib=rb-4.0.3&auto=format&fit=crop&w=600&q=80",
                    "https://images.unsplash.com/photo-1515286576774-4b5b5c90d968?ixlib=rb-4.0.3&auto=format&fit=crop&w=600&q=80",
                    "https://images.unsplash.com/photo-1513542789411-b6a5d4f31634?ixlib=rb-4.0.3&auto=format&fit=crop&w=600&q=80"
                ]
            },
            {
                id: 2,
                name: "Agenda Creativa 2024",
                category: "escolar",
                price: 22.50,
                image: "https://images.unsplash.com/photo-1544816155-12df9643f363?ixlib=rb-4.0.3&auto=format&fit=crop&w=600&q=80",
                desc: "Planifica tu año con estilo y mucho color. Tapa dura, hojas de 90g y stickers incluidos para decorar tus días importantes."
            },
            {
                id: 3,
                name: "Kit de Scrapbooking",
                category: "manualidades",
                price: 35.00,
                image: "https://images.unsplash.com/photo-1520695027581-2248530491fb?ixlib=rb-4.0.3&auto=format&fit=crop&w=600&q=80",
                desc: "Papeles, stickers y tijeras decorativas. Todo lo necesario para crear álbumes de recuerdos únicos.",
                gallery: [
                    "https://images.unsplash.com/photo-1520695027581-2248530491fb?ixlib=rb-4.0.3&auto=format&fit=crop&w=600&q=80",
                    "https://images.unsplash.com/photo-1456086272160-b28b3a456cc1?ixlib=rb-4.0.3&auto=format&fit=crop&w=600&q=80"
                ]
            },
            {
                id: 4,
                name: "Caja Sorpresa Regalo",
                category: "regalos",
                price: 45.00,
                image: "https://images.unsplash.com/photo-1549465220-1a8b9238cd48?ixlib=rb-4.0.3&auto=format&fit=crop&w=600&q=80",
                desc: "Perfecta para cumpleaños. Totalmente personalizada con dulces, globos y un mensaje especial a tu elección."
            },
            {
                id: 5,
                name: "Cartuchera Holográfica",
                category: "escolar",
                price: 12.00,
                image: "https://images.unsplash.com/photo-1566895391206-8b383860b093?ixlib=rb-4.0.3&auto=format&fit=crop&w=600&q=80",
                desc: "Brillante y espaciosa para todos tus útiles. Material resistente al agua y fácil de limpiar."
            },
            {
                id: 6,
                name: "Pinturas Acrílicas Set",
                category: "manualidades",
                price: 18.00,
                image: "https://images.unsplash.com/photo-1513364776144-60967b0f800f?ixlib=rb-4.0.3&auto=format&fit=crop&w=600&q=80",
                desc: "12 colores vibrantes para tus obras de arte. Alta pigmentación y secado rápido."
            },
            {
                id: 7,
                name: "Taza Personalizada",
                category: "regalos",
                price: 10.00,
                image: "https://images.unsplash.com/photo-1514228742587-6b1558fcca3d?ixlib=rb-4.0.3&auto=format&fit=crop&w=600&q=80",
                desc: "Con tu nombre o frase favorita. Cerámica de alta calidad apta para microondas."
            },
            {
                id: 8,
                name: "Mochila Pastel",
                category: "escolar",
                price: 40.00,
                image: "https://images.unsplash.com/photo-1553062407-98eeb64c6a62?ixlib=rb-4.0.3&auto=format&fit=crop&w=600&q=80",
                desc: "Resistente y con compartimento para laptop. Correas acolchadas para mayor comodidad."
            }
        ];

        // --- SISTEMA DE ALMACENAMIENTO (LocalStorage) ---
        // Intentar cargar productos guardados, si no existen, usar los por defecto
        let products = [];
        try {
            const storedProducts = localStorage.getItem('baugilu_products');
            if (storedProducts) {
                products = JSON.parse(storedProducts);
            } else {
                products = [...defaultProducts]; // Copia de los por defecto
            }
        } catch (e) {
            console.error("Error cargando productos:", e);
            products = [...defaultProducts];
        }

        let cart = [];

        // Función para guardar cambios en el navegador
        function saveProductsToStorage() {
            try {
                localStorage.setItem('baugilu_products', JSON.stringify(products));
            } catch (e) {
                console.error("Error guardando en localStorage:", e);
                // Si falla (probablemente por límite de espacio con imágenes base64), avisar al usuario
                if (e.name === 'QuotaExceededError') {
                    showToast("⚠️ Espacio lleno: Sube imágenes más pequeñas");
                }
            }
        }

        // --- Init ---
        document.addEventListener('DOMContentLoaded', () => {
            renderProducts('todos');
        });

        // --- Helper: Read File as Base64 ---
        function readFileAsDataURL(file) {
            return new Promise((resolve, reject) => {
                const reader = new FileReader();
                reader.onload = () => resolve(reader.result);
                reader.onerror = reject;
                reader.readAsDataURL(file);
            });
        }

        function previewImage(input, previewId) {
            const preview = document.getElementById(previewId);
            if (input.files && input.files[0]) {
                const reader = new FileReader();
                reader.onload = function(e) {
                    preview.src = e.target.result;
                    preview.classList.remove('hidden');
                }
                reader.readAsDataURL(input.files[0]);
            }
        }

        function previewGallery(input, previewId) {
            const container = document.getElementById(previewId);
            container.innerHTML = '';
            if (input.files) {
                Array.from(input.files).forEach(file => {
                    const reader = new FileReader();
                    reader.onload = function(e) {
                        const img = document.createElement('img');
                        img.src = e.target.result;
                        img.className = 'h-16 w-16 object-cover rounded border border-gray-200';
                        container.appendChild(img);
                    }
                    reader.readAsDataURL(file);
                });
            }
        }

        // --- Service Page Logic ---
        function openServicePage(serviceKey) {
            const data = serviceData[serviceKey];
            if (!data) return;

            document.getElementById('service-page-title').innerText = data.title;
            document.getElementById('service-page-desc').innerHTML = data.description;
            document.getElementById('service-hero-img').src = data.heroImage;

            const featuresList = document.getElementById('service-features-list');
            featuresList.innerHTML = '';
            data.features.forEach(item => {
                const div = document.createElement('div');
                div.className = "flex items-start gap-3 text-gray-700 bg-white/50 p-3 rounded-lg border border-brand-yellow/30";
                div.innerHTML = `<i class="fa-solid fa-check-circle text-brand-purple mt-1 flex-shrink-0"></i> <span>${item}</span>`;
                featuresList.appendChild(div);
            });

            const galleryGrid = document.getElementById('service-gallery-grid');
            galleryGrid.innerHTML = '';
            data.gallery.forEach(imgSrc => {
                const img = document.createElement('img');
                img.src = imgSrc;
                img.className = "w-full h-48 object-cover rounded-xl shadow-md hover:scale-[1.02] transition duration-300";
                galleryGrid.appendChild(img);
            });
            
            document.getElementById('service-page').classList.remove('hidden');
            document.body.style.overflow = 'hidden'; 
        }

        function closeServicePage() {
            document.getElementById('service-page').classList.add('hidden');
            document.body.style.overflow = '';
        }

        // --- Functions ---

        function toggleAdminMode() {
            if (isAdmin) {
                isAdmin = false;
                document.getElementById('admin-btn-text').innerText = "Acceso Admin";
                document.getElementById('add-product-btn').classList.add('hidden');
                showToast("Modo Admin Cerrado");
                
                const currentFilter = document.querySelector('.filter-btn.active')?.dataset.category || 'todos';
                renderProducts(currentFilter);
            } else {
                document.getElementById('admin-login-modal').classList.remove('hidden');
                document.getElementById('admin-pass-input').value = '';
                document.getElementById('admin-pass-input').focus();
            }
        }

        function closeAdminLogin() {
            document.getElementById('admin-login-modal').classList.add('hidden');
        }

        function checkAdminLogin(event) {
            event.preventDefault();
            const pass = document.getElementById('admin-pass-input').value;
            
            if (pass === "admin123") {
                isAdmin = true;
                document.getElementById('admin-btn-text').innerText = "Salir Admin";
                document.getElementById('add-product-btn').classList.remove('hidden');
                
                const currentFilter = document.querySelector('.filter-btn.active')?.dataset.category || 'todos';
                renderProducts(currentFilter);
                
                closeAdminLogin();
                showToast("¡Bienvenido Admin!");
            } else {
                const input = document.getElementById('admin-pass-input');
                input.classList.add('border-red-500', 'text-red-500');
                setTimeout(() => input.classList.remove('border-red-500', 'text-red-500'), 500);
                showToast("Contraseña incorrecta");
            }
        }

        function toggleMobileMenu() {
            const menu = document.getElementById('mobile-menu');
            menu.classList.toggle('hidden');
        }

        function filterProducts(category) {
            const buttons = document.querySelectorAll('.filter-btn');
            buttons.forEach(btn => {
                if(btn.dataset.category === category) {
                    btn.classList.remove('bg-white', 'text-gray-600');
                    btn.classList.add('bg-brand-dark', 'text-white', 'shadow-md');
                } else {
                    btn.classList.add('bg-white', 'text-gray-600');
                    btn.classList.remove('bg-brand-dark', 'text-white', 'shadow-md');
                }
            });

            renderProducts(category);
        }

        function renderProducts(filter) {
            const container = document.getElementById('product-grid');
            container.innerHTML = '';

            const filtered = filter === 'todos' 
                ? products 
                : products.filter(p => p.category === filter);

            filtered.forEach(product => {
                const card = document.createElement('div');
                card.className = "bg-white rounded-2xl shadow-sm hover:shadow-xl transition overflow-hidden group border border-gray-100 flex flex-col h-full relative";
                
                const hasGallery = product.gallery && product.gallery.length > 0;
                const galleryBadge = hasGallery ? 
                    `<span class="absolute top-2 right-2 bg-black/50 text-white text-xs px-2 py-1 rounded-full pointer-events-none z-10"><i class="fa-solid fa-images"></i> +${product.gallery.length}</span>` : '';

                const editButton = isAdmin ? `
                    <button onclick="openEditProductModal(event, ${product.id})" class="absolute top-2 left-2 bg-yellow-400 text-white p-2 rounded-full shadow-lg hover:bg-yellow-500 z-20 transition transform hover:scale-110" title="Editar Producto">
                        <i class="fa-solid fa-pen"></i>
                    </button>
                ` : '';

                card.innerHTML = `
                    <div class="relative h-64 overflow-hidden cursor-pointer" onclick="openProductDetails(${product.id})">
                        <img src="${product.image}" alt="${product.name}" class="w-full h-full object-cover group-hover:scale-105 transition duration-500">
                        ${galleryBadge}
                        ${editButton}
                    </div>
                    <div class="p-6 flex flex-col flex-1">
                        <div class="flex justify-between items-start mb-2">
                            <span class="text-xs font-bold uppercase text-brand-purple tracking-wider bg-brand-purple/10 px-2 py-1 rounded">${product.category}</span>
                            <span class="font-bold text-lg text-brand-dark">$${product.price.toFixed(2)}</span>
                        </div>
                        <h3 class="text-lg font-bold mb-2 font-heading text-gray-800 cursor-pointer hover:text-brand-purple" onclick="openProductDetails(${product.id})">${product.name}</h3>
                        <p class="text-gray-500 text-sm mb-4 line-clamp-2 flex-1">${product.desc}</p>
                        <button onclick="addToCart(${product.id})" class="w-full py-2 border border-brand-dark text-brand-dark font-bold rounded-lg hover:bg-brand-dark hover:text-white transition text-sm mt-auto">
                            Agregar al Carrito
                        </button>
                    </div>
                `;
                container.appendChild(card);
            });
        }

        // --- Edit Logic ---

        function openEditProductModal(event, id) {
            event.stopPropagation();
            const product = products.find(p => p.id === id);
            if (!product) return;

            document.getElementById('edit-id').value = product.id;
            document.getElementById('edit-name').value = product.name;
            document.getElementById('edit-category').value = product.category;
            document.getElementById('edit-price').value = product.price;
            document.getElementById('edit-desc').value = product.desc;
            
            const imgPreview = document.getElementById('edit-image-preview');
            imgPreview.src = product.image;
            imgPreview.classList.remove('hidden');
            
            const galleryPreview = document.getElementById('edit-gallery-preview');
            galleryPreview.innerHTML = '';
            if(product.gallery) {
                product.gallery.forEach(src => {
                    const img = document.createElement('img');
                    img.src = src;
                    img.className = 'h-16 w-16 object-cover rounded border border-gray-200';
                    galleryPreview.appendChild(img);
                });
            }

            document.getElementById('edit-image-file').value = '';
            document.getElementById('edit-gallery-files').value = '';

            document.getElementById('edit-product-modal').classList.remove('hidden');
        }

        function closeEditProductModal() {
            document.getElementById('edit-product-modal').classList.add('hidden');
        }

        async function handleUpdateProduct(event) {
            event.preventDefault();
            const form = event.target;
            const formData = new FormData(form);
            const id = parseInt(formData.get('id'));

            const index = products.findIndex(p => p.id === id);
            if (index === -1) return;

            let newImage = products[index].image;
            let newGallery = products[index].gallery || [];

            const imageFile = document.getElementById('edit-image-file').files[0];
            if (imageFile) {
                newImage = await readFileAsDataURL(imageFile);
            }

            const galleryFiles = document.getElementById('edit-gallery-files').files;
            if (galleryFiles.length > 0) {
                newGallery = []; 
                for(let file of galleryFiles) {
                    newGallery.push(await readFileAsDataURL(file));
                }
            }

            products[index] = {
                ...products[index],
                name: formData.get('name'),
                category: formData.get('category'),
                price: parseFloat(formData.get('price')),
                desc: formData.get('desc'),
                image: newImage,
                gallery: newGallery
            };

            // GUARDAR EN STORAGE
            saveProductsToStorage();

            closeEditProductModal();
            showToast("¡Producto actualizado!");
            
            const currentFilter = document.querySelector('.filter-btn.active')?.dataset.category || 'todos';
            renderProducts(currentFilter);
        }

        // --- Existing Functions (Cart, Details, etc.) ---

        function addToCart(id) {
            const product = products.find(p => p.id === id);
            const existing = cart.find(item => item.id === id);

            if (existing) {
                existing.qty++;
            } else {
                cart.push({ ...product, qty: 1 });
            }

            updateCartUI();
            showToast(`¡${product.name} agregado!`);
            
            const cartIcons = document.querySelectorAll('.fa-cart-shopping');
            cartIcons.forEach(icon => {
                icon.classList.add('animate-bounce-short');
                setTimeout(() => icon.classList.remove('animate-bounce-short'), 300);
            });
        }

        function removeFromCart(id) {
            cart = cart.filter(item => item.id !== id);
            updateCartUI();
        }

        function changeQty(id, change) {
            const item = cart.find(i => i.id === id);
            if (item) {
                item.qty += change;
                if (item.qty <= 0) removeFromCart(id);
                else updateCartUI();
            }
        }

        function updateCartUI() {
            const totalQty = cart.reduce((acc, item) => acc + item.qty, 0);
            document.getElementById('cart-count').innerText = totalQty;
            document.getElementById('cart-count-mobile').innerText = totalQty;
            document.getElementById('details-cart-count').innerText = totalQty;

            const container = document.getElementById('cart-items-container');
            const emptyState = document.getElementById('cart-empty-state');
            
            if (cart.length === 0) {
                container.innerHTML = '';
                container.appendChild(emptyState);
                emptyState.style.display = 'flex';
                document.getElementById('cart-subtotal').innerText = '$0.00';
                return;
            }

            emptyState.style.display = 'none';
            container.innerHTML = '';

            let total = 0;

            cart.forEach(item => {
                total += item.price * item.qty;
                const div = document.createElement('div');
                div.className = "flex gap-4 p-3 bg-white border border-gray-100 rounded-xl shadow-sm";
                div.innerHTML = `
                    <img src="${item.image}" class="w-16 h-16 rounded-lg object-cover">
                    <div class="flex-1">
                        <h4 class="font-bold text-sm text-brand-dark line-clamp-1">${item.name}</h4>
                        <div class="text-xs text-gray-500 mb-2">$${item.price.toFixed(2)} unit.</div>
                        <div class="flex items-center gap-3">
                            <button onclick="changeQty(${item.id}, -1)" class="w-6 h-6 rounded-full bg-gray-100 hover:bg-gray-200 flex items-center justify-center text-xs">-</button>
                            <span class="text-sm font-bold w-4 text-center">${item.qty}</span>
                            <button onclick="changeQty(${item.id}, 1)" class="w-6 h-6 rounded-full bg-gray-100 hover:bg-gray-200 flex items-center justify-center text-xs">+</button>
                        </div>
                    </div>
                    <div class="flex flex-col justify-between items-end">
                        <button onclick="removeFromCart(${item.id})" class="text-gray-400 hover:text-red-500 text-xs"><i class="fa-solid fa-trash"></i></button>
                        <span class="font-bold text-brand-purple">$${(item.price * item.qty).toFixed(2)}</span>
                    </div>
                `;
                container.appendChild(div);
            });

            document.getElementById('cart-subtotal').innerText = '$' + total.toFixed(2);
        }

        function toggleCart() {
            const modal = document.getElementById('cart-modal');
            modal.classList.toggle('hidden');
        }

        function showToast(message) {
            const x = document.getElementById("toast");
            x.innerText = message;
            x.className = "show";
            setTimeout(function(){ x.className = x.className.replace("show", ""); }, 3000);
        }

        // --- Product Details Logic ---
        function openProductDetails(id) {
            currentDetailId = id;
            const product = products.find(p => p.id === id);
            
            document.getElementById('detail-title').innerText = product.name;
            document.getElementById('detail-category').innerText = product.category;
            document.getElementById('detail-desc').innerText = product.desc;
            document.getElementById('detail-price').innerText = `$${product.price.toFixed(2)}`;
            document.getElementById('detail-price-old').innerText = `$${(product.price * 1.2).toFixed(2)}`;
            document.getElementById('detail-qty').value = 1;
            
            const mainImg = document.getElementById('detail-main-image');
            mainImg.src = product.image;
            
            const galleryContainer = document.getElementById('detail-gallery');
            galleryContainer.innerHTML = '';
            
            const allImages = [product.image];
            if (product.gallery && product.gallery.length > 0) {
                allImages.push(...product.gallery);
            }
            
            allImages.forEach((imgSrc, index) => {
                const thumb = document.createElement('img');
                thumb.src = imgSrc;
                thumb.className = `w-20 h-20 object-cover rounded-lg cursor-pointer border-2 hover:border-brand-purple transition ${index === 0 ? 'border-brand-purple' : 'border-transparent'}`;
                thumb.onclick = () => {
                    document.getElementById('detail-main-image').src = imgSrc;
                    Array.from(galleryContainer.children).forEach(c => {
                        c.classList.remove('border-brand-purple');
                        c.classList.add('border-transparent');
                    });
                    thumb.classList.remove('border-transparent');
                    thumb.classList.add('border-brand-purple');
                };
                galleryContainer.appendChild(thumb);
            });

            document.getElementById('product-details-modal').classList.remove('hidden');
            document.body.style.overflow = 'hidden';
        }

        function closeProductDetails() {
            document.getElementById('product-details-modal').classList.add('hidden');
            document.body.style.overflow = ''; 
            currentDetailId = null;
        }

        function adjustDetailQty(amount) {
            const input = document.getElementById('detail-qty');
            let val = parseInt(input.value);
            val += amount;
            if (val < 1) val = 1;
            input.value = val;
        }

        function addToCartFromDetail() {
            if (!currentDetailId) return;
            const qty = parseInt(document.getElementById('detail-qty').value);
            const product = products.find(p => p.id === currentDetailId);
            const existing = cart.find(item => item.id === currentDetailId);

            if (existing) {
                existing.qty += qty;
            } else {
                cart.push({ ...product, qty: qty });
            }
            
            updateCartUI();
            showToast(`¡${qty}x ${product.name} agregados!`);
            closeProductDetails();
            
            const cartIcons = document.querySelectorAll('.fa-cart-shopping');
            cartIcons.forEach(icon => {
                icon.classList.add('animate-bounce-short');
                setTimeout(() => icon.classList.remove('animate-bounce-short'), 300);
            });
        }

        function buyNowFromDetail() {
            addToCartFromDetail();
            openPaymentModal();
        }

        // --- Payment & Checkout Logic ---

        function checkout() {
            openPaymentModal();
        }

        function openPaymentModal() {
            if(cart.length === 0) return;
            toggleCart();
            closeProductDetails();
            const modal = document.getElementById('payment-modal');
            modal.classList.remove('hidden');
            updatePaymentInfo();
            
            const totalUSD = cart.reduce((acc, i) => acc + (i.price * i.qty), 0);
            const totalVES = totalUSD * exchangeRate;
            document.getElementById('pay-total-usd').innerText = `$${totalUSD.toFixed(2)}`;
            document.getElementById('pay-total-ves').innerText = `Bs ${totalVES.toFixed(2)}`;
        }

        function closePaymentModal() {
            document.getElementById('payment-modal').classList.add('hidden');
        }

        function updatePaymentInfo() {
            const method = document.querySelector('input[name="payment_method"]:checked').value;
            const detailsDiv = document.getElementById('payment-details');
            let html = '';
            
            if (method === 'Pago Móvil') {
                html = `
                    <div class="space-y-1">
                        <p class="font-bold text-brand-dark">Datos para Pago Móvil:</p>
                        <div class="grid grid-cols-3 gap-2 mt-2">
                            <div class="text-gray-500">Banco:</div>
                            <div class="col-span-2 font-medium">${pagoMovilData.banco}</div>
                            <div class="text-gray-500">Teléfono:</div>
                            <div class="col-span-2 font-medium">${pagoMovilData.telefono}</div>
                            <div class="text-gray-500">Cédula:</div>
                            <div class="col-span-2 font-medium">${pagoMovilData.cedula}</div>
                        </div>
                        <p class="text-xs text-brand-pink mt-2">Tasa de cambio: ${exchangeRate.toFixed(2)} Bs/$</p>
                    </div>
                `;
            } else if (method === 'PayPal') {
                html = `
                    <div class="space-y-2 text-center">
                        <p class="text-gray-600">Realiza tu pago al siguiente correo:</p>
                        <p class="font-bold text-lg text-blue-600 select-all">${paypalEmail}</p>
                        <p class="text-xs text-gray-400">Recuerda calcular la comisión si aplica.</p>
                        <a href="https://paypal.me/tuusuario" target="_blank" class="inline-block mt-2 text-xs text-blue-500 hover:underline">Ir a PayPal.me</a>
                    </div>
                `;
            } else if (method === 'Tarjeta') {
                html = `
                    <div class="text-center py-2">
                        <i class="fa-regular fa-envelope-open text-3xl text-purple-300 mb-2"></i>
                        <p class="text-gray-600">Selecciona esta opción para solicitar un <span class="font-bold">Link de Pago</span> seguro.</p>
                        <p class="text-xs text-gray-400 mt-1">Te lo enviaremos por WhatsApp al confirmar el pedido.</p>
                    </div>
                `;
            }
            detailsDiv.innerHTML = html;
        }

        function finalizeOrder(event) {
            event.preventDefault();
            const method = document.querySelector('input[name="payment_method"]:checked').value;
            const ref = document.getElementById('payment-ref').value;
            const totalUSD = cart.reduce((acc, i) => acc + (i.price * i.qty), 0);
            const totalVES = (totalUSD * exchangeRate).toFixed(2);
            
            let msg = "¡Hola Creaciones Baugilù! 🎨\nMe gustaría realizar el siguiente pedido:\n\n";
            cart.forEach(item => {
                msg += `• ${item.qty}x ${item.name} ($${item.price})\n`;
            });
            msg += `\n*Total a pagar: $${totalUSD.toFixed(2)}*`;
            msg += `\n\n----------------\n`;
            msg += `💳 *Método de Pago:* ${method}\n`;
            
            if (method === 'Pago Móvil') {
                msg += `💰 *Monto en Bs:* ${totalVES}\n`;
            }
            if (ref) {
                msg += `🧾 *Referencia:* ${ref}\n`;
            } else {
                msg += `⏳ *Estado:* Pendiente de pago/confirmación\n`;
            }

            const encodedMsg = encodeURIComponent(msg);
            const phoneNumber = "584142497952"; 
            window.open(`https://wa.me/${phoneNumber}?text=${encodedMsg}`, '_blank');
            
            cart = [];
            updateCartUI();
            closePaymentModal();
            showToast("¡Pedido enviado a WhatsApp!");
        }

        async function handleContact(event) {
            event.preventDefault();
            const form = event.target;
            const loadingOverlay = document.getElementById('form-loading');
            const successOverlay = document.getElementById('form-success');
            
            loadingOverlay.classList.remove('hidden');
            loadingOverlay.classList.add('flex');
            
            // Simular envío
            try {
                await new Promise(resolve => setTimeout(resolve, 2000));
                
                loadingOverlay.classList.add('hidden');
                loadingOverlay.classList.remove('flex');
                
                successOverlay.classList.remove('hidden');
                successOverlay.classList.add('flex');
                
                form.reset();
                showToast("Mensaje enviado correctamente");
                
            } catch (error) {
                console.error("Error al enviar", error);
                loadingOverlay.classList.add('hidden');
                alert("Hubo un error al enviar el mensaje. Por favor intenta nuevamente.");
            }
        }

        function resetContactForm() {
            document.getElementById('form-success').classList.add('hidden');
            document.getElementById('form-success').classList.remove('flex');
        }

        // --- Add Product Logic ---
        function openAddProductModal() {
            document.getElementById('add-product-modal').classList.remove('hidden');
        }

        function closeAddProductModal() {
            document.getElementById('add-product-modal').classList.add('hidden');
        }

        async function handleNewProduct(event) {
            event.preventDefault();
            const form = event.target;
            const formData = new FormData(form);
            
            const imageFile = document.getElementById('add-image-file').files[0];
            let imageUrl = "https://via.placeholder.com/300"; 
            
            if (imageFile) {
                imageUrl = await readFileAsDataURL(imageFile);
            }

            const galleryFiles = document.getElementById('add-gallery-files').files;
            let gallery = [];
            
            if (galleryFiles.length > 0) {
                for(let file of galleryFiles) {
                    gallery.push(await readFileAsDataURL(file));
                }
            }
            
            const newProduct = {
                id: Date.now(),
                name: formData.get('name'),
                category: formData.get('category'),
                price: parseFloat(formData.get('price')),
                desc: formData.get('desc'),
                image: imageUrl,
                gallery: gallery
            };
            
            products.unshift(newProduct);
            
            // GUARDAR EN STORAGE
            saveProductsToStorage();

            const currentFilter = document.querySelector('.filter-btn.active')?.dataset.category || 'todos';
            renderProducts(currentFilter);
            
            closeAddProductModal();
            form.reset();
            document.getElementById('add-image-preview').classList.add('hidden');
            document.getElementById('add-gallery-preview').innerHTML = '';
            
            showToast("¡Producto agregado exitosamente!");
            document.getElementById('catalogo').scrollIntoView({ behavior: 'smooth' });
        }

        // --- AI Assistant Logic ---
        
        function toggleAIChat() {
            const chatModal = document.getElementById('ai-chat-modal');
            chatModal.classList.toggle('hidden');
            if(!chatModal.classList.contains('hidden')) {
                setTimeout(() => document.getElementById('ai-user-input').focus(), 100);
                scrollToBottom();
            }
        }

        function scrollToBottom() {
            const container = document.getElementById('ai-chat-messages');
            container.scrollTop = container.scrollHeight;
        }

        function sendQuickPrompt(text) {
            document.getElementById('ai-user-input').value = text;
            handleAIChat(new Event('submit'));
        }

        async function handleAIChat(event) {
            event.preventDefault();
            const input = document.getElementById('ai-user-input');
            const message = input.value.trim();
            const sendBtn = document.getElementById('ai-send-btn');
            
            if (!message) return;

            addMessageToChat('user', message);
            input.value = '';
            input.disabled = true;
            sendBtn.disabled = true;
            document.getElementById('ai-suggestions').style.display = 'none';

            const loadingId = addLoadingIndicator();
            scrollToBottom();

            try {
                const storeContext = `
                    Eres el "Asistente Creativo" de Creaciones Baugilù, una tienda de manualidades, útiles escolares y regalos personalizados.
                    
                    Tus servicios principales son:
                    1. Papelería Creativa: Cuadernos, agendas, etiquetas, toppers (todo personalizado).
                    2. Talleres: Cursos de Cameo (plotter), diseño en Canva, tareas académicas y creación de logotipos.
                    3. Arreglos Sorpresa: Para Cumpleaños, San Valentín, Navidad, etc.
                    4. Venta de productos: Útiles escolares kawaii, kits de arte, bolsos.

                    Tu tono debe ser: Amable, entusiasta (usa emojis ✨🎨), servicial y experto en manualidades.
                    
                    Objetivo: Ayudar al usuario con ideas de regalos, redacción de mensajes para tarjetas o dudas sobre nuestros servicios. Siempre intenta redirigirlos a comprar un producto o servicio de la tienda de forma sutil.
                    
                    Productos actuales en catálogo (ejemplos): Set Escolar Kawaii ($15), Agenda 2024 ($22.50), Kit Scrapbooking ($35), Arreglos Sorpresa ($45).
                    
                    Si el usuario solicita visualizar, ver, generar o crear una imagen de un arreglo, manualidad o producto personalizado (que no sea una foto real del catálogo), responde ÚNICAMENTE con el marcador: [GENERAR_IMAGEN: <descripción detallada en inglés del objeto>].
                    Ejemplo: Usuario: "Quiero ver un ramo de rosas azules" -> Respuesta: "[GENERAR_IMAGEN: A beautiful bouquet of eternal blue roses with silver ribbons, soft lighting, professional photography]"
                    Si no es una solicitud de imagen, responde normalmente.
                    Responde de forma concisa (máximo 3 párrafos cortos).
                `;

                const response = await fetch(`https://generativelanguage.googleapis.com/v1beta/models/gemini-2.5-flash-preview-09-2025:generateContent?key=${apiKey}`, {
                    method: 'POST',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify({
                        contents: [{
                            role: "user",
                            parts: [{ text: storeContext + "\n\nConsulta del usuario: " + message }]
                        }]
                    })
                });

                const data = await response.json();
                document.getElementById(loadingId).remove();

                if (data.error) throw new Error(data.error.message);

                const aiText = data.candidates[0].content.parts[0].text;

                if (aiText.includes('[GENERAR_IMAGEN:')) {
                    const match = aiText.match(/\[GENERAR_IMAGEN: (.*?)\]/);
                    if (match) {
                        const imagePrompt = match[1];
                        addMessageToChat('ai', "🎨 Creando diseño exclusivo para ti... dame un momento.");
                        const imgLoadingId = addLoadingIndicator();
                        
                        try {
                            const imgResponse = await fetch(`https://generativelanguage.googleapis.com/v1beta/models/imagen-4.0-generate-001:predict?key=${apiKey}`, {
                                method: 'POST',
                                headers: { 'Content-Type': 'application/json' },
                                body: JSON.stringify({
                                    instances: [{ prompt: imagePrompt }],
                                    parameters: { sampleCount: 1 }
                                })
                            });
                            
                            const imgData = await imgResponse.json();
                            document.getElementById(imgLoadingId).remove();

                            if(imgData.predictions) {
                                const imgUrl = `data:image/png;base64,${imgData.predictions[0].bytesBase64Encoded}`;
                                addImageToChat('ai', imgUrl);
                                addMessageToChat('ai', "¿Qué te parece esta opción? Podemos personalizarla con los colores que gustes.");
                            } else {
                                throw new Error("No image data");
                            }
                        } catch (e) {
                            console.error(e);
                            document.getElementById(imgLoadingId)?.remove();
                            addMessageToChat('ai', "Lo siento, tuve un problema generando la imagen. Pero puedo describírtela o buscar referencias.");
                        }
                        return; 
                    }
                }

                addMessageToChat('ai', aiText);

            } catch (error) {
                console.error("AI Error:", error);
                document.getElementById(loadingId)?.remove();
                addMessageToChat('ai', "¡Ups! Tuve un pequeño bloqueo creativo. 🤯 ¿Podrías intentar preguntar de nuevo?");
            } finally {
                input.disabled = false;
                sendBtn.disabled = false;
                input.focus();
                scrollToBottom();
            }
        }

        function addMessageToChat(role, text) {
            const container = document.getElementById('ai-chat-messages');
            const div = document.createElement('div');
            
            if (role === 'user') {
                div.className = "flex justify-end";
                div.innerHTML = `
                    <div class="bg-brand-purple text-white p-3 rounded-2xl rounded-tr-none shadow-sm text-sm max-w-[85%]">
                        ${text}
                    </div>
                `;
            } else {
                const htmlContent = marked.parse(text);
                div.className = "flex items-start gap-2";
                div.innerHTML = `
                    <div class="w-8 h-8 bg-brand-purple rounded-full flex items-center justify-center text-white flex-shrink-0 text-xs mt-1">
                        <i class="fa-solid fa-wand-magic-sparkles"></i>
                    </div>
                    <div class="bg-white p-3 rounded-2xl rounded-tl-none shadow-sm text-sm text-gray-700 border border-gray-100 prose prose-sm max-w-[85%] leading-relaxed">
                        ${htmlContent}
                    </div>
                `;
            }
            
            container.appendChild(div);
            scrollToBottom();
        }

        function addImageToChat(role, imgUrl) {
            const container = document.getElementById('ai-chat-messages');
            const div = document.createElement('div');
            div.className = "flex items-start gap-2";
            div.innerHTML = `
                <div class="w-8 h-8 bg-brand-purple rounded-full flex items-center justify-center text-white flex-shrink-0 text-xs mt-1">
                    <i class="fa-solid fa-wand-magic-sparkles"></i>
                </div>
                <div class="bg-white p-2 rounded-2xl rounded-tl-none shadow-sm text-sm text-gray-700 border border-gray-100 max-w-[85%] relative">
                    <div class="generated-image-container">
                        <img src="${imgUrl}" class="w-full h-auto rounded-lg" alt="Generated Image">
                        <a href="${imgUrl}" download="baugilu-design-${Date.now()}.png" class="download-btn" title="Descargar Imagen">
                            <i class="fa-solid fa-download"></i>
                        </a>
                    </div>
                </div>
            `;
            container.appendChild(div);
            scrollToBottom();
        }

        function addLoadingIndicator() {
            const container = document.getElementById('ai-chat-messages');
            const id = 'loading-' + Date.now();
            const div = document.createElement('div');
            div.id = id;
            div.className = "flex items-start gap-2";
            div.innerHTML = `
                <div class="w-8 h-8 bg-brand-purple rounded-full flex items-center justify-center text-white flex-shrink-0 text-xs">
                    <i class="fa-solid fa-wand-magic-sparkles"></i>
                </div>
                <div class="bg-white p-4 rounded-2xl rounded-tl-none shadow-sm border border-gray-100 flex gap-1">
                    <div class="w-2 h-2 bg-brand-pink rounded-full typing-dot"></div>
                    <div class="w-2 h-2 bg-brand-purple rounded-full typing-dot"></div>
                    <div class="w-2 h-2 bg-brand-blue rounded-full typing-dot"></div>
                </div>
            `;
            container.appendChild(div);
            return id;
        }

        async function generateDescription(nameId, catId, targetId) {
            const name = document.getElementById(nameId).value;
            const category = document.getElementById(catId).value;
            const target = document.getElementById(targetId);
            
            if(!name) {
                alert("Por favor escribe el nombre del producto primero.");
                return;
            }

            target.value = "✨ Generando descripción mágica...";
            target.disabled = true;

            try {
                const prompt = `Escribe una descripción corta, atractiva y vendedora (máximo 2 párrafos) para un producto de manualidades/papelería llamado "${name}" de la categoría "${category}". Usa emojis y un tono amable y creativo.`;
                
                const response = await fetch(`https://generativelanguage.googleapis.com/v1beta/models/gemini-2.5-flash-preview-09-2025:generateContent?key=${apiKey}`, {
                    method: 'POST',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify({ contents: [{ parts: [{ text: prompt }] }] })
                });

                const data = await response.json();
                target.value = data.candidates[0].content.parts[0].text;
            } catch (error) {
                console.error(error);
                target.value = "Error al generar. Intenta de nuevo.";
            } finally {
                target.disabled = false;
            }
        }
    </script>
</body>
</html>
