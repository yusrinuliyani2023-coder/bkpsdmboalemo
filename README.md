<!DOCTYPE html>
<html lang="id" class="h-full">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>BKPSDM Kabupaten Boalemo - Portal Berita 2025</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css" rel="stylesheet">
    <style>
        body {
            box-sizing: border-box;
        }
        .fade-in {
            animation: fadeIn 0.5s ease-in;
        }
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }
        .slide-in {
            animation: slideIn 0.3s ease-out;
        }
        @keyframes slideIn {
            from { transform: translateX(-100%); }
            to { transform: translateX(0); }
        }
    </style>
</head>
<body class="h-full bg-gray-50 font-sans">
    <!-- Navigation -->
    <nav class="bg-green-800 shadow-lg sticky top-0 z-50">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="flex justify-between items-center h-16">
                <div class="flex items-center space-x-4">
                    <div class="flex items-center space-x-3">
                        <div class="w-10 h-10 bg-white rounded-full flex items-center justify-center">
                            <img src="boalemo.png.png" width="30" height="30">
                        </div>
                        <div class="text-white">
                            <h1 class="font-bold text-lg">BKPSDM</h1>
                            <p class="text-xs text-blue-200">Kab. Boalemo</p>
                        </div>
                    </div>
                </div>
                
                <div class="hidden md:flex items-center space-x-6">
                    <a href="#" onclick="showSection('beranda')" class="text-white hover:text-blue-200 transition-colors">Beranda</a>
                    <a href="#" onclick="showSection('berita')" class="text-white hover:text-blue-200 transition-colors">Berita</a>
                    <a href="#" onclick="showSection('pengumuman')" class="text-white hover:text-blue-200 transition-colors">Pengumuman</a>
                    <a href="#" onclick="showSection('layanan')" class="text-white hover:text-blue-200 transition-colors">Layanan</a>
                    <a href="#" onclick="showSection('galeri')" class="text-white hover:text-blue-200 transition-colors">Galeri</a>
                    <a href="#" onclick="showSection('profil')" class="text-white hover:text-blue-200 transition-colors">Profil</a>
                    <a href="#" id="navUsersLink" onclick="showSection('users')" class="hidden text-white hover:text-blue-200 transition-colors">Kelola Pengguna</a>
                </div>

                <div class="flex items-center space-x-4">
                    <!-- User Profile Menu (when logged in) -->
                    <div id="userProfileMenu" class="hidden relative">
                        <button id="profileMenuBtn" onclick="toggleProfileMenu()" class="flex items-center space-x-2 bg-blue-700 hover:bg-blue-800 text-white px-4 py-2 rounded-lg transition-colors">
                            <div class="w-8 h-8 bg-white rounded-full flex items-center justify-center">
                                <i class="fas fa-user text-blue-700 text-sm"></i>
                            </div>
                            <span id="userNameDisplay" class="hidden md:block"></span>
                            <i class="fas fa-chevron-down text-sm"></i>
                        </button>
                        
                        <!-- Dropdown Menu -->
                        <div id="profileDropdown" class="hidden absolute right-0 mt-2 w-48 bg-white rounded-lg shadow-lg border border-gray-200 z-50">
                            <div class="py-2">
                                <div class="px-4 py-2 border-b border-gray-200">
                                    <p class="text-sm font-semibold text-gray-800" id="dropdownUserName"></p>
                                    <p class="text-xs text-gray-500" id="dropdownUserRole"></p>
                                </div>
                                <button onclick="showSection('profil'); toggleProfileMenu();" class="w-full text-left px-4 py-2 text-sm text-gray-700 hover:bg-gray-100 transition-colors">
                                    <i class="fas fa-user mr-2"></i>Lihat Profil
                                </button>
                                <button id="navEditProfileBtn" onclick="showEditProfile(); toggleProfileMenu();" class="hidden w-full text-left px-4 py-2 text-sm text-gray-700 hover:bg-gray-100 transition-colors">
                                    <i class="fas fa-edit mr-2"></i>Edit Profil
                                </button>
                                <button id="navEditPhotoBtn" onclick="showEditPhoto(); toggleProfileMenu();" class="hidden w-full text-left px-4 py-2 text-sm text-gray-700 hover:bg-gray-100 transition-colors">
                                    <i class="fas fa-camera mr-2"></i>Edit Foto
                                </button>
                                <button id="navUsersBtn" onclick="showSection('users'); toggleProfileMenu();" class="hidden w-full text-left px-4 py-2 text-sm text-gray-700 hover:bg-gray-100 transition-colors">
                                    <i class="fas fa-users mr-2"></i>Kelola Pengguna
                                </button>
                                <div class="border-t border-gray-200 mt-2 pt-2">
                                    <button onclick="logout(); toggleProfileMenu();" class="w-full text-left px-4 py-2 text-sm text-red-600 hover:bg-red-50 transition-colors">
                                        <i class="fas fa-sign-out-alt mr-2"></i>Logout
                                    </button>
                                </div>
                            </div>
                        </div>
                    </div>
                    
                    <!-- Login Button (when not logged in) -->
                    <button id="loginBtn" onclick="showLogin()" class="bg-blue-600 hover:bg-blue-700 text-white px-4 py-2 rounded-lg transition-colors">
                        <i class="fas fa-sign-in-alt mr-2"></i>Login
                    </button>
                </div>
            </div>
        </div>
    </nav>

    <!-- Login Modal -->
    <div id="loginModal" class="hidden fixed inset-0 bg-black bg-opacity-50 z-50 flex items-center justify-center">
        <div class="bg-white rounded-lg p-8 max-w-md w-full mx-4 slide-in">
            <div class="text-center mb-6">
                <h2 class="text-2xl font-bold text-gray-800">Login Portal</h2>
                <p class="text-gray-600 mt-2">Masuk ke sistem BKPSDM Boalemo</p>
            </div>
            
            <form onsubmit="handleLogin(event)">
                <div class="mb-4">
                    <label class="block text-gray-700 text-sm font-bold mb-2">Username</label>
                    <input type="text" id="username" class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:outline-none focus:border-blue-500" required>
                </div>
                
                <div class="mb-6">
                    <label class="block text-gray-700 text-sm font-bold mb-2">Password</label>
                    <input type="password" id="password" class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:outline-none focus:border-blue-500" required>
                </div>
                
                <div class="flex justify-between items-center">
                    <button type="button" onclick="hideLogin()" class="bg-gray-500 hover:bg-gray-600 text-white px-4 py-2 rounded-lg transition-colors">
                        Batal
                    </button>
                    <button type="submit" class="bg-blue-600 hover:bg-blue-700 text-white px-6 py-2 rounded-lg transition-colors">
                        Login
                    </button>
                </div>
            </form>
            
            <div class="mt-4 p-3 bg-blue-50 rounded-lg text-sm">
                <p class="font-semibold text-blue-800">Demo Login:</p>
                <p class="text-blue-600">Super Admin: superadmin / super123</p>
                <p class="text-blue-600">Admin: admin / admin123</p>
                <p class="text-blue-600">User: user / user123</p>
            </div>
        </div>
    </div>

    <!-- Main Content -->
    <main class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-8">
        <!-- User Role Indicator -->
        <div id="roleIndicator" class="hidden mb-6 p-4 bg-green-100 border border-green-300 rounded-lg">
            <div class="flex items-center">
                <i class="fas fa-user-check text-green-600 mr-3"></i>
                <span id="roleText" class="text-green-800 font-semibold"></span>
            </div>
        </div>

        <!-- Beranda Section -->
        <div id="berandaSection" class="fade-in">
            <!-- Hero Section -->
            <div class="bg-gradient-to-r from-blue-800 to-green-600 rounded-lg text-white p-8 mb-8">
                <div class="max-w-4xl">
                    <h1 class="text-4xl font-bold mb-4">Selamat Datang di Portal BKPSDM</h1>
                    <h2 class="text-2xl mb-4">Kabupaten Boalemo</h2>
                    <p class="text-xl text-blue-100 mb-6">Badan Kepegawaian dan Pengembangan Sumber Daya Manusia - Informasi Terkini Tahun 2025</p>
                    <button onclick="showSection('berita')" class="bg-white text-blue-800 px-6 py-3 rounded-lg font-semibold hover:bg-blue-50 transition-colors">
                        Lihat Berita Terbaru
                    </button>
                </div>
            </div>

            <!-- Quick Stats -->
            <div class="grid grid-cols-1 md:grid-cols-4 gap-6 mb-8">
                <div class="bg-white p-6 rounded-lg shadow-md text-center">
                    <i class="fas fa-newspaper text-3xl text-blue-600 mb-3"></i>
                    <h3 class="text-2xl font-bold text-gray-800" id="totalBerita">12</h3>
                    <p class="text-gray-600">Total Berita</p>
                </div>
                <div class="bg-white p-6 rounded-lg shadow-md text-center">
                    <i class="fas fa-bullhorn text-3xl text-green-600 mb-3"></i>
                    <h3 class="text-2xl font-bold text-gray-800" id="totalPengumuman">8</h3>
                    <p class="text-gray-600">Pengumuman</p>
                </div>
                <div class="bg-white p-6 rounded-lg shadow-md text-center relative">
                    <i class="fas fa-users text-3xl text-purple-600 mb-3"></i>
                    <h3 class="text-2xl font-bold text-gray-800" id="totalPegawai">1,247</h3>
                    <p class="text-gray-600">Total Pegawai</p>
                    <p class="text-xs text-gray-500 mt-1">ASN, PPPK & PPPK Paruh Waktu</p>
                    <button id="editPegawaiBtn" onclick="showEditPegawai()" class="hidden absolute top-2 right-2 text-purple-600 hover:text-purple-800 transition-colors">
                        <i class="fas fa-edit text-sm"></i>
                    </button>
                </div>
                <div class="bg-white p-6 rounded-lg shadow-md text-center relative">
                    <i class="fas fa-calendar text-3xl text-orange-600 mb-3"></i>
                    <h3 class="text-2xl font-bold text-gray-800" id="activeYear">2025</h3>
                    <p class="text-gray-600">Tahun Aktif</p>
                    <button id="editYearBtn" onclick="showEditYear()" class="hidden absolute top-2 right-2 text-orange-600 hover:text-orange-800 transition-colors">
                        <i class="fas fa-edit text-sm"></i>
                    </button>
                </div>
            </div>

            <!-- Gallery Slider -->
            <div class="bg-white rounded-lg shadow-md overflow-hidden mb-8">
                <div class="p-6 border-b border-gray-200">
                    <div class="flex justify-between items-center">
                        <h2 class="text-2xl font-bold text-gray-800">Galeri & Pengumuman Terbaru</h2>
                        <div class="flex space-x-4">
                            <button onclick="showSection('galeri')" class="text-purple-600 hover:text-purple-800 text-sm font-semibold transition-colors">
                                Galeri <i class="fas fa-arrow-right ml-1"></i>
                            </button>
                            <button onclick="showSection('pengumuman')" class="text-green-600 hover:text-green-800 text-sm font-semibold transition-colors">
                                Pengumuman <i class="fas fa-arrow-right ml-1"></i>
                            </button>
                        </div>
                    </div>
                </div>
                
                <div class="relative h-80 overflow-hidden">
                    <!-- Slider Container -->
                    <div id="homepageSlider" class="relative h-full">
                        <!-- Slides will be populated by JavaScript -->
                    </div>
                    
                    <!-- Navigation Arrows -->
                    <button onclick="changeHomepageSlide(-1)" class="absolute left-4 top-1/2 transform -translate-y-1/2 bg-black bg-opacity-50 hover:bg-opacity-75 text-white p-2 rounded-full transition-all z-10">
                        <i class="fas fa-chevron-left"></i>
                    </button>
                    <button onclick="changeHomepageSlide(1)" class="absolute right-4 top-1/2 transform -translate-y-1/2 bg-black bg-opacity-50 hover:bg-opacity-75 text-white p-2 rounded-full transition-all z-10">
                        <i class="fas fa-chevron-right"></i>
                    </button>
                    
                    <!-- Slide Indicators -->
                    <div class="absolute bottom-4 left-1/2 transform -translate-x-1/2 flex space-x-2 z-10" id="homepageSlideIndicators">
                        <!-- Indicators will be populated by JavaScript -->
                    </div>
                    
                    <!-- Content Type Badge -->
                    <div class="absolute top-4 left-4 z-10" id="homepageContentBadge">
                        <!-- Badge will be populated by JavaScript -->
                    </div>
                </div>
            </div>

            <!-- Latest News Preview -->
            <div class="bg-white rounded-lg shadow-md p-6">
                <h2 class="text-2xl font-bold text-gray-800 mb-6">Berita Terbaru</h2>
                <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6" id="latestNews">
                    <!-- News items will be populated by JavaScript -->
                </div>
            </div>
        </div>

        <!-- Berita Section -->
        <div id="beritaSection" class="hidden">
            <div class="flex justify-between items-center mb-6">
                <h1 class="text-3xl font-bold text-gray-800">Portal Berita</h1>
                <button id="addNewsBtn" onclick="showAddNews()" class="hidden bg-blue-600 hover:bg-blue-700 text-white px-4 py-2 rounded-lg transition-colors">
                    <i class="fas fa-plus mr-2"></i>Tambah Berita
                </button>
            </div>

            <!-- News Grid -->
            <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6" id="newsGrid">
                <!-- News items will be populated by JavaScript -->
            </div>
        </div>

        <!-- Pengumuman Section -->
        <div id="pengumumanSection" class="hidden">
            <div class="flex justify-between items-center mb-6">
                <h1 class="text-3xl font-bold text-gray-800">Pengumuman</h1>
                <button id="addAnnouncementBtn" onclick="showAddAnnouncement()" class="hidden bg-green-600 hover:bg-green-700 text-white px-4 py-2 rounded-lg transition-colors">
                    <i class="fas fa-plus mr-2"></i>Tambah Pengumuman
                </button>
            </div>

            <!-- Announcements List -->
            <div class="space-y-4" id="announcementsList">
                <!-- Announcements will be populated by JavaScript -->
            </div>
        </div>

        <!-- Layanan Section -->
        <div id="layananSection" class="hidden">
            <div class="flex justify-between items-center mb-6">
                <h1 class="text-3xl font-bold text-gray-800">Layanan BKPSDM</h1>
                <button id="addServiceBtn" onclick="showAddService()" class="hidden bg-indigo-600 hover:bg-indigo-700 text-white px-4 py-2 rounded-lg transition-colors">
                    <i class="fas fa-plus mr-2"></i>Tambah Layanan
                </button>
            </div>

            <!-- Service Filters -->
            <div class="mb-6">
                <div class="flex flex-wrap gap-2">
                    <button onclick="filterServices('all')" class="service-filter-btn bg-indigo-600 text-white px-4 py-2 rounded-lg text-sm font-medium transition-colors">
                        Semua Layanan
                    </button>
                    <button onclick="filterServices('kepegawaian')" class="service-filter-btn bg-gray-200 text-gray-700 hover:bg-gray-300 px-4 py-2 rounded-lg text-sm font-medium transition-colors">
                        Kepegawaian
                    </button>
                    <button onclick="filterServices('diklat')" class="service-filter-btn bg-gray-200 text-gray-700 hover:bg-gray-300 px-4 py-2 rounded-lg text-sm font-medium transition-colors">
                        Diklat & Pengembangan
                    </button>
                    <button onclick="filterServices('informasi')" class="service-filter-btn bg-gray-200 text-gray-700 hover:bg-gray-300 px-4 py-2 rounded-lg text-sm font-medium transition-colors">
                        Informasi
                    </button>
                    <button onclick="filterServices('konsultasi')" class="service-filter-btn bg-gray-200 text-gray-700 hover:bg-gray-300 px-4 py-2 rounded-lg text-sm font-medium transition-colors">
                        Konsultasi
                    </button>
                </div>
            </div>

            <!-- Services Grid -->
            <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6" id="servicesGrid">
                <!-- Services will be populated by JavaScript -->
            </div>
        </div>

        <!-- Galeri Section -->
        <div id="galeriSection" class="hidden">
            <div class="flex justify-between items-center mb-6">
                <h1 class="text-3xl font-bold text-gray-800">Galeri Kegiatan</h1>
                <button id="addGalleryBtn" onclick="showAddGallery()" class="hidden bg-purple-600 hover:bg-purple-700 text-white px-4 py-2 rounded-lg transition-colors">
                    <i class="fas fa-plus mr-2"></i>Tambah Foto
                </button>
            </div>

            <!-- Gallery Slider -->
            <div class="bg-white rounded-lg shadow-md overflow-hidden mb-8">
                <div class="relative h-96 overflow-hidden">
                    <!-- Slider Container -->
                    <div id="gallerySlider" class="relative h-full">
                        <!-- Slides will be populated by JavaScript -->
                    </div>
                    
                    <!-- Navigation Arrows -->
                    <button onclick="changeSlide(-1)" class="absolute left-4 top-1/2 transform -translate-y-1/2 bg-black bg-opacity-50 hover:bg-opacity-75 text-white p-3 rounded-full transition-all z-10">
                        <i class="fas fa-chevron-left"></i>
                    </button>
                    <button onclick="changeSlide(1)" class="absolute right-4 top-1/2 transform -translate-y-1/2 bg-black bg-opacity-50 hover:bg-opacity-75 text-white p-3 rounded-full transition-all z-10">
                        <i class="fas fa-chevron-right"></i>
                    </button>
                    
                    <!-- Slide Indicators -->
                    <div class="absolute bottom-4 left-1/2 transform -translate-x-1/2 flex space-x-2 z-10" id="slideIndicators">
                        <!-- Indicators will be populated by JavaScript -->
                    </div>
                </div>
            </div>

            <!-- Gallery Grid -->
            <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6" id="galleryGrid">
                <!-- Gallery items will be populated by JavaScript -->
            </div>
        </div>

        <!-- Users Section -->
        <div id="usersSection" class="hidden">
            <div class="flex justify-between items-center mb-6">
                <h1 class="text-3xl font-bold text-gray-800">Kelola Pengguna</h1>
                <button id="addUserBtn" onclick="showAddUser()" class="hidden bg-green-600 hover:bg-green-700 text-white px-4 py-2 rounded-lg transition-colors">
                    <i class="fas fa-user-plus mr-2"></i>Tambah Pengguna
                </button>
            </div>

            <!-- Users Table -->
            <div class="bg-white rounded-lg shadow-md overflow-hidden">
                <div class="overflow-x-auto">
                    <table class="min-w-full divide-y divide-gray-200">
                        <thead class="bg-gray-50">
                            <tr>
                                <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Pengguna</th>
                                <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Role</th>
                                <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Email</th>
                                <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Tanggal Dibuat</th>
                                <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Aksi</th>
                            </tr>
                        </thead>
                        <tbody id="usersTableBody" class="bg-white divide-y divide-gray-200">
                            <!-- Users will be populated by JavaScript -->
                        </tbody>
                    </table>
                </div>
            </div>
        </div>

        <!-- Profil Section -->
        <div id="profilSection" class="hidden">
            <div class="flex justify-between items-center mb-6">
                <h1 class="text-3xl font-bold text-gray-800">Profil BKPSDM Kabupaten Boalemo</h1>
                <button id="editProfileBtn" onclick="showEditProfile()" class="hidden bg-blue-600 hover:bg-blue-700 text-white px-4 py-2 rounded-lg transition-colors">
                    <i class="fas fa-edit mr-2"></i>Edit Profil
                </button>
            </div>
            
            <!-- Profile Photo Section -->
            <div class="bg-white rounded-lg shadow-md p-8 mb-6">
                <div class="flex flex-col md:flex-row items-center md:items-start gap-6">
                    <div class="text-center">
                        <div class="relative">
                            <div id="profilePhoto" class="w-32 h-32 bg-gradient-to-br from-blue-600 to-blue-800 rounded-full flex items-center justify-center text-white text-4xl font-bold shadow-lg">
                                BKPSDM
                            </div>
                            <button id="editPhotoBtn" onclick="showEditPhoto()" class="hidden absolute -bottom-2 -right-2 bg-blue-600 hover:bg-blue-700 text-white w-8 h-8 rounded-full flex items-center justify-center transition-colors">
                                <i class="fas fa-camera text-xs"></i>
                            </button>
                        </div>
                        <h3 class="text-xl font-bold text-gray-800 mt-4">BKPSDM Kabupaten Boalemo</h3>
                        <p class="text-gray-600">Badan Kepegawaian dan Pengembangan SDM</p>
                    </div>
                    
                    <div class="flex-1">
                        <h2 class="text-2xl font-bold text-blue-800 mb-4">Tentang Kami</h2>
                        <p class="text-gray-700 leading-relaxed">
                            BKPSDM Kabupaten Boalemo adalah lembaga yang bertanggung jawab dalam pengelolaan kepegawaian dan pengembangan sumber daya manusia aparatur di lingkungan Pemerintah Kabupaten Boalemo. Kami berkomitmen untuk menciptakan aparatur yang profesional, kompeten, dan berintegritas tinggi.
                        </p>
                    </div>
                </div>
            </div>
            
            <div class="bg-white rounded-lg shadow-md p-8 mb-6">
                <h2 class="text-2xl font-bold text-blue-800 mb-4">Visi</h2>
                <p id="visiText" class="text-gray-700 mb-6">BKPSDM Boalemo adalah meningkatkan profesionalitas dan kompetensi Aparatur Sipil Negara (ASN). Misi utamanya adalah mewujudkan ASN yang memiliki pengetahuan dan keterampilan sesuai kompetensinya, meningkatkan kualitas manajemen kepegawaian, serta membangun tata kelola informasi kepegawaian yang lengkap dan akurat. BKPSDM Boalemo adalah meningkatkan profesionalitas dan kompetensi Aparatur Sipil Negara (ASN). Misi utamanya adalah mewujudkan ASN yang memiliki pengetahuan dan keterampilan sesuai kompetensinya, meningkatkan kualitas manajemen kepegawaian, serta membangun tata kelola informasi kepegawaian yang lengkap dan akurat.</p>
                
                <h2 class="text-2xl font-bold text-blue-800 mb-4">Misi</h2>
                <ul id="misiList" class="text-gray-700 space-y-2">
                    <li class="flex items-start"><i class="fas fa-check text-green-600 mr-3 mt-1"></i>Mengembangkan sistem manajemen ASN yang transparan dan akuntabel</li>
                    <li class="flex items-start"><i class="fas fa-check text-green-600 mr-3 mt-1"></i>Meningkatkan kompetensi dan profesionalisme ASN</li>
                    <li class="flex items-start"><i class="fas fa-check text-green-600 mr-3 mt-1"></i>Mewujudkan pelayanan publik yang berkualitas</li>
                </ul>
            </div>
            
            <div class="bg-white rounded-lg shadow-md p-8">
                <div class="flex justify-between items-center mb-6">
                    <h2 class="text-2xl font-bold text-blue-800">Struktur Organisasi</h2>
                    <button id="editStructureBtn" onclick="showEditStructure()" class="hidden bg-green-600 hover:bg-green-700 text-white px-3 py-1 rounded text-sm transition-colors">
                        <i class="fas fa-edit mr-1"></i>Edit
                    </button>
                </div>
                <div id="structureChart" class="overflow-x-auto">
                    <!-- Structure chart will be populated by JavaScript -->
                </div>
            </div>
        </div>
    </main>

    <!-- Add News Modal -->
    <div id="addNewsModal" class="hidden fixed inset-0 bg-black bg-opacity-50 z-50 flex items-center justify-center">
        <div class="bg-white rounded-lg p-8 max-w-2xl w-full mx-4 max-h-[90vh] overflow-y-auto">
            <h2 class="text-2xl font-bold text-gray-800 mb-6">Tambah Berita Baru</h2>
            
            <form onsubmit="handleAddNews(event)">
                <div class="mb-4">
                    <label class="block text-gray-700 text-sm font-bold mb-2">Judul Berita</label>
                    <input type="text" id="newsTitle" class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:outline-none focus:border-blue-500" required>
                </div>
                
                <div class="mb-4">
                    <label class="block text-gray-700 text-sm font-bold mb-2">Kategori</label>
                    <select id="newsCategory" class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:outline-none focus:border-blue-500" required>
                        <option value="">Pilih Kategori</option>
                        <option value="Kepegawaian">Kepegawaian</option>
                        <option value="Pengembangan SDM">Pengembangan SDM</option>
                        <option value="Pelayanan">Pelayanan</option>
                        <option value="Berita Umum">Berita Umum</option>
                        <option value="Kegiatan">Kegiatan</option>
                        <option value="Informasi">Informasi</option>
                    </select>
                </div>
                
                <div class="mb-4">
                    <label class="block text-gray-700 text-sm font-bold mb-2">Tanggal Berita</label>
                    <input type="date" id="newsDate" class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:outline-none focus:border-blue-500" required>
                </div>
                
                <div class="mb-4">
                    <label class="block text-gray-700 text-sm font-bold mb-2">Gambar Berita (Opsional)</label>
                    <input type="file" id="newsImage" accept="image/*" onchange="handleNewsImageUpload(event)" class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:outline-none focus:border-blue-500">
                    <p class="text-gray-500 text-xs mt-1">Maksimal 5MB. Format: JPG, PNG, GIF</p>
                    <div id="newsImagePreview" class="hidden mt-3">
                        <img id="newsImagePreviewImg" src="" alt="Preview" class="max-w-full h-48 object-cover rounded-lg border">
                        <button type="button" onclick="removeNewsImage()" class="mt-2 text-red-600 hover:text-red-800 text-sm">
                            <i class="fas fa-trash mr-1"></i>Hapus Gambar
                        </button>
                    </div>
                </div>
                
                <div class="mb-6">
                    <label class="block text-gray-700 text-sm font-bold mb-2">Isi Berita</label>
                    <textarea id="newsContent" rows="6" class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:outline-none focus:border-blue-500" required></textarea>
                </div>
                
                <div class="flex justify-between">
                    <button type="button" onclick="hideAddNews()" class="bg-gray-500 hover:bg-gray-600 text-white px-4 py-2 rounded-lg transition-colors">
                        Batal
                    </button>
                    <button type="submit" class="bg-blue-600 hover:bg-blue-700 text-white px-6 py-2 rounded-lg transition-colors">
                        Publikasikan
                    </button>
                </div>
            </form>
        </div>
    </div>

    <!-- Add Announcement Modal -->
    <div id="addAnnouncementModal" class="hidden fixed inset-0 bg-black bg-opacity-50 z-50 flex items-center justify-center">
        <div class="bg-white rounded-lg p-8 max-w-2xl w-full mx-4 max-h-[90vh] overflow-y-auto">
            <h2 class="text-2xl font-bold text-gray-800 mb-6">Tambah Pengumuman Baru</h2>
            
            <form onsubmit="handleAddAnnouncement(event)">
                <div class="mb-4">
                    <label class="block text-gray-700 text-sm font-bold mb-2">Judul Pengumuman</label>
                    <input type="text" id="announcementTitle" class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:outline-none focus:border-blue-500" required>
                </div>
                
                <div class="mb-4">
                    <label class="block text-gray-700 text-sm font-bold mb-2">Kategori</label>
                    <select id="announcementCategory" class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:outline-none focus:border-blue-500" required>
                        <option value="">Pilih Kategori</option>
                        <option value="Kepegawaian">Kepegawaian</option>
                        <option value="Pengembangan SDM">Pengembangan SDM</option>
                        <option value="Pelayanan">Pelayanan</option>
                        <option value="Pengumuman Umum">Pengumuman Umum</option>
                        <option value="Seleksi">Seleksi</option>
                        <option value="Diklat">Diklat</option>
                    </select>
                </div>
                
                <div class="mb-4">
                    <label class="block text-gray-700 text-sm font-bold mb-2">Prioritas</label>
                    <select id="announcementPriority" class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:outline-none focus:border-blue-500" required>
                        <option value="">Pilih Prioritas</option>
                        <option value="Tinggi">Tinggi</option>
                        <option value="Sedang">Sedang</option>
                        <option value="Rendah">Rendah</option>
                    </select>
                </div>
                
                <div class="mb-4">
                    <label class="block text-gray-700 text-sm font-bold mb-2">Tanggal Pengumuman</label>
                    <input type="date" id="announcementDate" class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:outline-none focus:border-blue-500" required>
                </div>
                
                <div class="mb-4">
                    <label class="block text-gray-700 text-sm font-bold mb-2">Gambar Pengumuman (Opsional)</label>
                    <input type="file" id="announcementImage" accept="image/*" onchange="handleAnnouncementImageUpload(event)" class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:outline-none focus:border-blue-500">
                    <p class="text-gray-500 text-xs mt-1">Maksimal 5MB. Format: JPG, PNG, GIF</p>
                    <div id="announcementImagePreview" class="hidden mt-3">
                        <img id="announcementImagePreviewImg" src="" alt="Preview" class="max-w-full h-48 object-cover rounded-lg border">
                        <button type="button" onclick="removeAnnouncementImage()" class="mt-2 text-red-600 hover:text-red-800 text-sm">
                            <i class="fas fa-trash mr-1"></i>Hapus Gambar
                        </button>
                    </div>
                </div>
                
                <div class="mb-4">
                    <label class="block text-gray-700 text-sm font-bold mb-2">Dokumen PDF (Opsional)</label>
                    <input type="file" id="announcementPDF" accept=".pdf" onchange="handleAnnouncementPDFUpload(event)" class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:outline-none focus:border-blue-500">
                    <p class="text-gray-500 text-xs mt-1">Maksimal 10MB. Format: PDF</p>
                    <div id="announcementPDFPreview" class="hidden mt-3 p-3 bg-gray-50 rounded-lg border">
                        <div class="flex items-center justify-between">
                            <div class="flex items-center">
                                <i class="fas fa-file-pdf text-red-500 text-2xl mr-3"></i>
                                <div>
                                    <p id="announcementPDFName" class="text-sm font-medium text-gray-800"></p>
                                    <p id="announcementPDFSize" class="text-xs text-gray-500"></p>
                                </div>
                            </div>
                            <button type="button" onclick="removeAnnouncementPDF()" class="text-red-600 hover:text-red-800 text-sm">
                                <i class="fas fa-trash mr-1"></i>Hapus
                            </button>
                        </div>
                    </div>
                </div>
                
                <div class="mb-6">
                    <label class="block text-gray-700 text-sm font-bold mb-2">Isi Pengumuman</label>
                    <textarea id="announcementContent" rows="6" class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:outline-none focus:border-blue-500" required></textarea>
                </div>
                
                <div class="flex justify-between">
                    <button type="button" onclick="hideAddAnnouncement()" class="bg-gray-500 hover:bg-gray-600 text-white px-4 py-2 rounded-lg transition-colors">
                        Batal
                    </button>
                    <button type="submit" class="bg-green-600 hover:bg-green-700 text-white px-6 py-2 rounded-lg transition-colors">
                        Publikasikan
                    </button>
                </div>
            </form>
        </div>
    </div>

    <!-- Edit Photo Modal -->
    <div id="editPhotoModal" class="hidden fixed inset-0 bg-black bg-opacity-50 z-50 flex items-center justify-center">
        <div class="bg-white rounded-lg p-8 max-w-md w-full mx-4">
            <h2 class="text-2xl font-bold text-gray-800 mb-6">Edit Foto Profil</h2>
            
            <div class="text-center mb-6">
                <div id="previewPhoto" class="w-32 h-32 bg-gradient-to-br from-blue-600 to-blue-800 rounded-full flex items-center justify-center text-white text-4xl font-bold shadow-lg mx-auto mb-4 overflow-hidden">
                    BKPSDM
                </div>
                <p class="text-gray-600 text-sm mb-4">Pilih foto dari galeri atau gunakan gaya default:</p>
                
                <!-- File Input -->
                <input type="file" id="photoFileInput" accept="image/*" onchange="handlePhotoUpload(event)" class="hidden">
                <button onclick="document.getElementById('photoFileInput').click()" class="bg-blue-600 hover:bg-blue-700 text-white px-6 py-3 rounded-lg transition-colors mb-4 w-full">
                    <i class="fas fa-camera mr-2"></i>Pilih Foto dari Galeri
                </button>
                
                <div class="border-t pt-4">
                    <p class="text-gray-600 text-sm mb-3">Atau pilih gaya default:</p>
                </div>
            </div>
            
            <div class="grid grid-cols-2 gap-4 mb-6">
                <button onclick="selectPhotoStyle('gradient')" class="photo-style-btn p-4 border-2 border-gray-300 rounded-lg hover:border-blue-500 transition-colors">
                    <div class="w-16 h-16 bg-gradient-to-br from-blue-600 to-blue-800 rounded-full flex items-center justify-center text-white text-sm font-bold mx-auto mb-2">
                        BKPSDM
                    </div>
                    <p class="text-xs text-gray-600">Gradient</p>
                </button>
                
                <button onclick="selectPhotoStyle('solid')" class="photo-style-btn p-4 border-2 border-gray-300 rounded-lg hover:border-blue-500 transition-colors">
                    <div class="w-16 h-16 bg-blue-700 rounded-full flex items-center justify-center text-white text-sm font-bold mx-auto mb-2">
                        BKPSDM
                    </div>
                    <p class="text-xs text-gray-600">Solid</p>
                </button>
                
                <button onclick="selectPhotoStyle('pattern')" class="photo-style-btn p-4 border-2 border-gray-300 rounded-lg hover:border-blue-500 transition-colors">
                    <div class="w-16 h-16 bg-blue-600 rounded-full flex items-center justify-center text-white text-sm font-bold mx-auto mb-2 relative overflow-hidden">
                        <div class="absolute inset-0 bg-blue-800 opacity-20" style="background-image: repeating-linear-gradient(45deg, transparent, transparent 2px, rgba(255,255,255,0.1) 2px, rgba(255,255,255,0.1) 4px);"></div>
                        BKPSDM
                    </div>
                    <p class="text-xs text-gray-600">Pattern</p>
                </button>
                
                <button onclick="selectPhotoStyle('icon')" class="photo-style-btn p-4 border-2 border-gray-300 rounded-lg hover:border-blue-500 transition-colors">
                    <div class="w-16 h-16 bg-blue-600 rounded-full flex items-center justify-center text-white mx-auto mb-2">
                        <i class="fas fa-building text-2xl"></i>
                    </div>
                    <p class="text-xs text-gray-600">Icon</p>
                </button>
            </div>
            
            <div class="flex justify-between">
                <button onclick="hideEditPhoto()" class="bg-gray-500 hover:bg-gray-600 text-white px-4 py-2 rounded-lg transition-colors">
                    Batal
                </button>
                <button onclick="savePhotoStyle()" class="bg-blue-600 hover:bg-blue-700 text-white px-6 py-2 rounded-lg transition-colors">
                    Simpan
                </button>
            </div>
        </div>
    </div>

    <!-- Edit Profile Modal -->
    <div id="editProfileModal" class="hidden fixed inset-0 bg-black bg-opacity-50 z-50 flex items-center justify-center">
        <div class="bg-white rounded-lg p-8 max-w-2xl w-full mx-4 max-h-[90vh] overflow-y-auto">
            <h2 class="text-2xl font-bold text-gray-800 mb-6">Edit Profil Organisasi</h2>
            
            <form onsubmit="handleEditProfile(event)">
                <div class="mb-4">
                    <label class="block text-gray-700 text-sm font-bold mb-2">Visi</label>
                    <textarea id="editVisi" rows="4" class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:outline-none focus:border-blue-500" required></textarea>
                </div>
                
                <div class="mb-6">
                    <label class="block text-gray-700 text-sm font-bold mb-2">Misi (pisahkan dengan enter untuk setiap poin)</label>
                    <textarea id="editMisi" rows="6" class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:outline-none focus:border-blue-500" required placeholder="Masukkan setiap misi dalam baris terpisah"></textarea>
                </div>
                
                <div class="flex justify-between">
                    <button type="button" onclick="hideEditProfile()" class="bg-gray-500 hover:bg-gray-600 text-white px-4 py-2 rounded-lg transition-colors">
                        Batal
                    </button>
                    <button type="submit" class="bg-blue-600 hover:bg-blue-700 text-white px-6 py-2 rounded-lg transition-colors">
                        Simpan
                    </button>
                </div>
            </form>
        </div>
    </div>

    <!-- Add User Modal -->
    <div id="addUserModal" class="hidden fixed inset-0 bg-black bg-opacity-50 z-50 flex items-center justify-center">
        <div class="bg-white rounded-lg p-8 max-w-md w-full mx-4">
            <h2 class="text-2xl font-bold text-gray-800 mb-6">Tambah Pengguna Baru</h2>
            
            <form onsubmit="handleAddUser(event)">
                <div class="mb-4">
                    <label class="block text-gray-700 text-sm font-bold mb-2">Nama Lengkap</label>
                    <input type="text" id="newUserName" class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:outline-none focus:border-blue-500" required>
                </div>
                
                <div class="mb-4">
                    <label class="block text-gray-700 text-sm font-bold mb-2">Username</label>
                    <input type="text" id="newUserUsername" class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:outline-none focus:border-blue-500" required>
                </div>
                
                <div class="mb-4">
                    <label class="block text-gray-700 text-sm font-bold mb-2">Email</label>
                    <input type="email" id="newUserEmail" class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:outline-none focus:border-blue-500" required>
                </div>
                
                <div class="mb-4">
                    <label class="block text-gray-700 text-sm font-bold mb-2">Password</label>
                    <input type="password" id="newUserPassword" class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:outline-none focus:border-blue-500" required>
                </div>
                
                <div class="mb-6">
                    <label class="block text-gray-700 text-sm font-bold mb-2">Role</label>
                    <select id="newUserRole" class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:outline-none focus:border-blue-500" required>
                        <option value="">Pilih Role</option>
                        <option value="admin">Admin</option>
                        <option value="user">User</option>
                    </select>
                </div>
                
                <div class="flex justify-between">
                    <button type="button" onclick="hideAddUser()" class="bg-gray-500 hover:bg-gray-600 text-white px-4 py-2 rounded-lg transition-colors">
                        Batal
                    </button>
                    <button type="submit" class="bg-green-600 hover:bg-green-700 text-white px-6 py-2 rounded-lg transition-colors">
                        Tambah Pengguna
                    </button>
                </div>
            </form>
        </div>
    </div>

    <!-- Edit Pegawai Modal -->
    <div id="editPegawaiModal" class="hidden fixed inset-0 bg-black bg-opacity-50 z-50 flex items-center justify-center">
        <div class="bg-white rounded-lg p-8 max-w-lg w-full mx-4">
            <h2 class="text-2xl font-bold text-gray-800 mb-6">Edit Data Pegawai</h2>
            
            <form onsubmit="handleEditPegawai(event)">
                <div class="grid grid-cols-1 md:grid-cols-2 gap-4 mb-6">
                    <div>
                        <label class="block text-gray-700 text-sm font-bold mb-2">ASN</label>
                        <input type="number" id="editASNCount" min="0" class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:outline-none focus:border-purple-500" required>
                        <p class="text-gray-500 text-xs mt-1">Aparatur Sipil Negara</p>
                    </div>
                    <div>
                        <label class="block text-gray-700 text-sm font-bold mb-2">PPPK</label>
                        <input type="number" id="editPPPKCount" min="0" class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:outline-none focus:border-purple-500" required>
                        <p class="text-gray-500 text-xs mt-1">Pegawai Pemerintah dengan Perjanjian Kerja</p>
                    </div>
                </div>
                
                <div class="mb-6">
                    <label class="block text-gray-700 text-sm font-bold mb-2">PPPK Paruh Waktu</label>
                    <input type="number" id="editPPPKParuhWaktuCount" min="0" class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:outline-none focus:border-purple-500" required>
                    <p class="text-gray-500 text-xs mt-1">PPPK dengan waktu kerja paruh waktu</p>
                </div>
                
                <div class="mb-6 p-4 bg-purple-50 rounded-lg border border-purple-200">
                    <div class="flex justify-between items-center">
                        <span class="text-purple-800 font-semibold">Total Pegawai:</span>
                        <span id="totalPegawaiPreview" class="text-purple-800 font-bold text-lg">0</span>
                    </div>
                </div>
                
                <div class="flex justify-between">
                    <button type="button" onclick="hideEditPegawai()" class="bg-gray-500 hover:bg-gray-600 text-white px-4 py-2 rounded-lg transition-colors">
                        Batal
                    </button>
                    <button type="submit" class="bg-purple-600 hover:bg-purple-700 text-white px-6 py-2 rounded-lg transition-colors">
                        Simpan
                    </button>
                </div>
            </form>
        </div>
    </div>

    <!-- Edit Year Modal -->
    <div id="editYearModal" class="hidden fixed inset-0 bg-black bg-opacity-50 z-50 flex items-center justify-center">
        <div class="bg-white rounded-lg p-8 max-w-md w-full mx-4">
            <h2 class="text-2xl font-bold text-gray-800 mb-6">Edit Tahun Aktif</h2>
            
            <form onsubmit="handleEditYear(event)">
                <div class="mb-6">
                    <label class="block text-gray-700 text-sm font-bold mb-2">Tahun Aktif</label>
                    <input type="number" id="editActiveYear" min="2020" max="2030" class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:outline-none focus:border-blue-500" required>
                    <p class="text-gray-500 text-xs mt-1">Masukkan tahun aktif sistem (2020-2030)</p>
                </div>
                
                <div class="flex justify-between">
                    <button type="button" onclick="hideEditYear()" class="bg-gray-500 hover:bg-gray-600 text-white px-4 py-2 rounded-lg transition-colors">
                        Batal
                    </button>
                    <button type="submit" class="bg-orange-600 hover:bg-orange-700 text-white px-6 py-2 rounded-lg transition-colors">
                        Simpan
                    </button>
                </div>
            </form>
        </div>
    </div>

    <!-- Add Gallery Modal -->
    <div id="addGalleryModal" class="hidden fixed inset-0 bg-black bg-opacity-50 z-50 flex items-center justify-center">
        <div class="bg-white rounded-lg p-8 max-w-2xl w-full mx-4 max-h-[90vh] overflow-y-auto">
            <h2 class="text-2xl font-bold text-gray-800 mb-6">Tambah Foto Galeri</h2>
            
            <form onsubmit="handleAddGallery(event)">
                <div class="mb-4">
                    <label class="block text-gray-700 text-sm font-bold mb-2">Judul Foto</label>
                    <input type="text" id="galleryTitle" class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:outline-none focus:border-purple-500" required>
                </div>
                
                <div class="mb-4">
                    <label class="block text-gray-700 text-sm font-bold mb-2">Kategori</label>
                    <select id="galleryCategory" class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:outline-none focus:border-purple-500" required>
                        <option value="">Pilih Kategori</option>
                        <option value="Kegiatan Diklat">Kegiatan Diklat</option>
                        <option value="Rapat Koordinasi">Rapat Koordinasi</option>
                        <option value="Pelayanan Publik">Pelayanan Publik</option>
                        <option value="Upacara">Upacara</option>
                        <option value="Sosialisasi">Sosialisasi</option>
                        <option value="Kunjungan">Kunjungan</option>
                    </select>
                </div>
                
                <div class="mb-4">
                    <label class="block text-gray-700 text-sm font-bold mb-2">Tanggal Kegiatan</label>
                    <input type="date" id="galleryDate" class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:outline-none focus:border-purple-500" required>
                </div>
                
                <div class="mb-4">
                    <label class="block text-gray-700 text-sm font-bold mb-2">Foto Kegiatan</label>
                    <input type="file" id="galleryImage" accept="image/*" onchange="handleGalleryImageUpload(event)" class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:outline-none focus:border-purple-500" required>
                    <p class="text-gray-500 text-xs mt-1">Maksimal 5MB. Format: JPG, PNG, GIF</p>
                    <div id="galleryImagePreview" class="hidden mt-3">
                        <img id="galleryImagePreviewImg" src="" alt="Preview" class="max-w-full h-48 object-cover rounded-lg border">
                        <button type="button" onclick="removeGalleryImage()" class="mt-2 text-red-600 hover:text-red-800 text-sm">
                            <i class="fas fa-trash mr-1"></i>Hapus Gambar
                        </button>
                    </div>
                </div>
                
                <div class="mb-6">
                    <label class="block text-gray-700 text-sm font-bold mb-2">Deskripsi Kegiatan</label>
                    <textarea id="galleryDescription" rows="4" class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:outline-none focus:border-purple-500" required></textarea>
                </div>
                
                <div class="flex justify-between">
                    <button type="button" onclick="hideAddGallery()" class="bg-gray-500 hover:bg-gray-600 text-white px-4 py-2 rounded-lg transition-colors">
                        Batal
                    </button>
                    <button type="submit" class="bg-purple-600 hover:bg-purple-700 text-white px-6 py-2 rounded-lg transition-colors">
                        Tambah ke Galeri
                    </button>
                </div>
            </form>
        </div>
    </div>

    <!-- Gallery View Modal -->
    <div id="galleryViewModal" class="hidden fixed inset-0 bg-black bg-opacity-75 z-50 flex items-center justify-center">
        <div class="bg-white rounded-lg max-w-4xl w-full mx-4 max-h-[90vh] overflow-hidden">
            <div class="flex">
                <!-- Image Section -->
                <div class="flex-1 h-96 overflow-hidden" id="galleryViewImage">
                    <!-- Image will be populated by JavaScript -->
                </div>
                
                <!-- Info Section -->
                <div class="w-80 p-6 bg-gray-50">
                    <div class="flex justify-between items-start mb-4">
                        <h3 id="galleryViewTitle" class="text-xl font-bold text-gray-800"></h3>
                        <button onclick="hideGalleryView()" class="text-gray-500 hover:text-gray-700 transition-colors">
                            <i class="fas fa-times text-xl"></i>
                        </button>
                    </div>
                    
                    <div class="mb-4">
                        <span id="galleryViewCategory" class="bg-purple-100 text-purple-800 text-sm font-semibold px-3 py-1 rounded"></span>
                    </div>
                    
                    <p id="galleryViewDescription" class="text-gray-600 mb-4"></p>
                    
                    <p id="galleryViewDate" class="text-sm text-gray-500 mb-6"></p>
                    
                    <button id="deleteGalleryBtn" onclick="deleteGalleryItem()" class="hidden w-full bg-red-600 hover:bg-red-700 text-white px-4 py-2 rounded-lg transition-colors">
                        <i class="fas fa-trash mr-2"></i>Hapus Foto
                    </button>
                </div>
            </div>
        </div>
    </div>

    <!-- Edit User Modal -->
    <div id="editUserModal" class="hidden fixed inset-0 bg-black bg-opacity-50 z-50 flex items-center justify-center">
        <div class="bg-white rounded-lg p-8 max-w-md w-full mx-4">
            <h2 class="text-2xl font-bold text-gray-800 mb-6">Edit Pengguna</h2>
            
            <form onsubmit="handleEditUser(event)">
                <input type="hidden" id="editUserId">
                
                <div class="mb-4">
                    <label class="block text-gray-700 text-sm font-bold mb-2">Nama Lengkap</label>
                    <input type="text" id="editUserName" class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:outline-none focus:border-blue-500" required>
                </div>
                
                <div class="mb-4">
                    <label class="block text-gray-700 text-sm font-bold mb-2">Username</label>
                    <input type="text" id="editUserUsername" class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:outline-none focus:border-blue-500" required>
                </div>
                
                <div class="mb-4">
                    <label class="block text-gray-700 text-sm font-bold mb-2">Email</label>
                    <input type="email" id="editUserEmail" class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:outline-none focus:border-blue-500" required>
                </div>
                
                <div class="mb-4">
                    <label class="block text-gray-700 text-sm font-bold mb-2">Password Baru (kosongkan jika tidak diubah)</label>
                    <input type="password" id="editUserPassword" class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:outline-none focus:border-blue-500">
                </div>
                
                <div class="mb-6">
                    <label class="block text-gray-700 text-sm font-bold mb-2">Role</label>
                    <select id="editUserRole" class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:outline-none focus:border-blue-500" required>
                        <option value="admin">Admin</option>
                        <option value="user">User</option>
                    </select>
                </div>
                
                <div class="flex justify-between">
                    <button type="button" onclick="hideEditUser()" class="bg-gray-500 hover:bg-gray-600 text-white px-4 py-2 rounded-lg transition-colors">
                        Batal
                    </button>
                    <button type="submit" class="bg-blue-600 hover:bg-blue-700 text-white px-6 py-2 rounded-lg transition-colors">
                        Simpan Perubahan
                    </button>
                </div>
            </form>
        </div>
    </div>

    <!-- Edit Structure Modal -->
    <div id="editStructureModal" class="hidden fixed inset-0 bg-black bg-opacity-50 z-50 flex items-center justify-center">
        <div class="bg-white rounded-lg p-8 max-w-4xl w-full mx-4 max-h-[90vh] overflow-y-auto">
            <h2 class="text-2xl font-bold text-gray-800 mb-6">Edit Struktur Organisasi</h2>
            
            <div id="structureEditor" class="space-y-6 mb-6">
                <!-- Structure editor items will be populated by JavaScript -->
            </div>
            
            <div class="flex justify-between items-center">
                <button onclick="addStructureItem()" class="bg-green-600 hover:bg-green-700 text-white px-4 py-2 rounded-lg transition-colors">
                    <i class="fas fa-plus mr-2"></i>Tambah Jabatan
                </button>
                <div class="flex space-x-2">
                    <button onclick="hideEditStructure()" class="bg-gray-500 hover:bg-gray-600 text-white px-4 py-2 rounded-lg transition-colors">
                        Batal
                    </button>
                    <button onclick="saveStructure()" class="bg-blue-600 hover:bg-blue-700 text-white px-6 py-2 rounded-lg transition-colors">
                        Simpan
                    </button>
                </div>
            </div>
        </div>
    </div>

    <!-- Add Service Modal -->
    <div id="addServiceModal" class="hidden fixed inset-0 bg-black bg-opacity-50 z-50 flex items-center justify-center">
        <div class="bg-white rounded-lg p-8 max-w-2xl w-full mx-4 max-h-[90vh] overflow-y-auto">
            <h2 class="text-2xl font-bold text-gray-800 mb-6">Tambah Layanan Baru</h2>
            
            <form onsubmit="handleAddService(event)">
                <div class="grid grid-cols-1 md:grid-cols-2 gap-6 mb-6">
                    <div>
                        <label class="block text-gray-700 text-sm font-bold mb-2">Nama Layanan</label>
                        <input type="text" id="serviceName" class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:outline-none focus:border-indigo-500" required>
                    </div>
                    <div>
                        <label class="block text-gray-700 text-sm font-bold mb-2">Kategori</label>
                        <select id="serviceCategory" class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:outline-none focus:border-indigo-500" required>
                            <option value="">Pilih Kategori</option>
                            <option value="kepegawaian">Kepegawaian</option>
                            <option value="diklat">Diklat & Pengembangan</option>
                            <option value="informasi">Informasi</option>
                            <option value="konsultasi">Konsultasi</option>
                        </select>
                    </div>
                </div>
                
                <div class="grid grid-cols-1 md:grid-cols-3 gap-6 mb-6">
                    <div>
                        <label class="block text-gray-700 text-sm font-bold mb-2">Jenis Layanan</label>
                        <select id="serviceType" class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:outline-none focus:border-indigo-500" required>
                            <option value="">Pilih Jenis</option>
                            <option value="online">Online</option>
                            <option value="offline">Offline</option>
                            <option value="hybrid">Online & Offline</option>
                        </select>
                    </div>
                    <div>
                        <label class="block text-gray-700 text-sm font-bold mb-2">Waktu Pelayanan</label>
                        <input type="text" id="serviceTime" placeholder="contoh: 1-2 hari kerja" class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:outline-none focus:border-indigo-500" required>
                    </div>
                    <div>
                        <label class="block text-gray-700 text-sm font-bold mb-2">Biaya</label>
                        <input type="text" id="serviceCost" placeholder="contoh: Gratis atau Rp 50.000" class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:outline-none focus:border-indigo-500" required>
                    </div>
                </div>
                
                <div class="mb-6">
                    <label class="block text-gray-700 text-sm font-bold mb-2">Deskripsi Layanan</label>
                    <textarea id="serviceDescription" rows="3" class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:outline-none focus:border-indigo-500" required></textarea>
                </div>
                
                <div class="mb-6">
                    <label class="block text-gray-700 text-sm font-bold mb-2">Persyaratan (pisahkan dengan enter)</label>
                    <textarea id="serviceRequirements" rows="4" placeholder="Masukkan setiap persyaratan dalam baris terpisah" class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:outline-none focus:border-indigo-500" required></textarea>
                </div>
                
                <div class="mb-6">
                    <label class="block text-gray-700 text-sm font-bold mb-2">Prosedur (pisahkan dengan enter)</label>
                    <textarea id="serviceProcedure" rows="4" placeholder="Masukkan setiap langkah prosedur dalam baris terpisah" class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:outline-none focus:border-indigo-500" required></textarea>
                </div>
                
                <div class="flex justify-between">
                    <button type="button" onclick="hideAddService()" class="bg-gray-500 hover:bg-gray-600 text-white px-4 py-2 rounded-lg transition-colors">
                        Batal
                    </button>
                    <button type="submit" class="bg-indigo-600 hover:bg-indigo-700 text-white px-6 py-2 rounded-lg transition-colors">
                        Tambah Layanan
                    </button>
                </div>
            </form>
        </div>
    </div>

    <!-- Service Detail Modal -->
    <div id="serviceDetailModal" class="hidden fixed inset-0 bg-black bg-opacity-50 z-50 flex items-center justify-center">
        <div class="bg-white rounded-lg max-w-4xl w-full mx-4 max-h-[90vh] overflow-hidden">
            <div class="flex">
                <!-- Main Content -->
                <div class="flex-1 p-8 overflow-y-auto max-h-[90vh]">
                    <div class="flex justify-between items-start mb-6">
                        <div>
                            <h2 id="serviceDetailTitle" class="text-2xl font-bold text-gray-800 mb-2"></h2>
                            <div class="flex flex-wrap gap-2 mb-4">
                                <span id="serviceDetailCategory" class="bg-indigo-100 text-indigo-800 text-sm font-semibold px-3 py-1 rounded"></span>
                                <span id="serviceDetailType" class="bg-green-100 text-green-800 text-sm font-semibold px-3 py-1 rounded"></span>
                            </div>
                        </div>
                        <button onclick="hideServiceDetail()" class="text-gray-500 hover:text-gray-700 transition-colors">
                            <i class="fas fa-times text-xl"></i>
                        </button>
                    </div>
                    
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-6 mb-6">
                        <div class="bg-gray-50 p-4 rounded-lg">
                            <h3 class="font-semibold text-gray-800 mb-2">Informasi Layanan</h3>
                            <div class="space-y-2 text-sm">
                                <div class="flex justify-between">
                                    <span class="text-gray-600">Waktu Pelayanan:</span>
                                    <span id="serviceDetailTime" class="font-medium text-gray-800"></span>
                                </div>
                                <div class="flex justify-between">
                                    <span class="text-gray-600">Biaya:</span>
                                    <span id="serviceDetailCost" class="font-semibold text-indigo-600"></span>
                                </div>
                            </div>
                        </div>
                        <div class="bg-gray-50 p-4 rounded-lg">
                            <h3 class="font-semibold text-gray-800 mb-2">Deskripsi</h3>
                            <p id="serviceDetailDescription" class="text-gray-700 text-sm leading-relaxed"></p>
                        </div>
                    </div>
                    
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                        <div>
                            <h3 class="text-lg font-semibold text-gray-800 mb-4">Persyaratan</h3>
                            <ul id="serviceDetailRequirements" class="space-y-2">
                                <!-- Requirements will be populated by JavaScript -->
                            </ul>
                        </div>
                        <div>
                            <h3 class="text-lg font-semibold text-gray-800 mb-4">Prosedur</h3>
                            <ol id="serviceDetailProcedure" class="space-y-2">
                                <!-- Procedure will be populated by JavaScript -->
                            </ol>
                        </div>
                    </div>
                    
                    <div class="mt-8 pt-6 border-t border-gray-200">
                        <div class="flex justify-between items-center">
                            <div class="text-sm text-gray-500">
                                <i class="fas fa-info-circle mr-1"></i>
                                Untuk informasi lebih lanjut, silakan hubungi BKPSDM Kabupaten Boalemo
                            </div>
                            <div class="flex space-x-2">
                                <button id="editServiceBtn" onclick="showEditService()" class="hidden bg-blue-600 hover:bg-blue-700 text-white px-4 py-2 rounded-lg transition-colors text-sm">
                                    <i class="fas fa-edit mr-1"></i>Edit
                                </button>
                                <button id="deleteServiceBtn" onclick="deleteCurrentService()" class="hidden bg-red-600 hover:bg-red-700 text-white px-4 py-2 rounded-lg transition-colors text-sm">
                                    <i class="fas fa-trash mr-1"></i>Hapus
                                </button>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <!-- Edit Structure Item Modal -->
    <div id="editStructureItemModal" class="hidden fixed inset-0 bg-black bg-opacity-50 z-50 flex items-center justify-center">
        <div class="bg-white rounded-lg p-8 max-w-2xl w-full mx-4 max-h-[90vh] overflow-y-auto">
            <h2 class="text-2xl font-bold text-gray-800 mb-6">Edit Jabatan</h2>
            
            <form onsubmit="handleEditStructureItem(event)">
                <input type="hidden" id="editStructureItemId">
                
                <div class="grid grid-cols-1 md:grid-cols-2 gap-6 mb-6">
                    <div>
                        <label class="block text-gray-700 text-sm font-bold mb-2">Nama Jabatan</label>
                        <input type="text" id="editStructurePosition" class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:outline-none focus:border-blue-500" required>
                    </div>
                    <div>
                        <label class="block text-gray-700 text-sm font-bold mb-2">Nama Pejabat</label>
                        <input type="text" id="editStructureName" class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:outline-none focus:border-blue-500" required>
                    </div>
                </div>

                <div class="mb-6">
                    <label class="block text-gray-700 text-sm font-bold mb-2">Foto Pejabat</label>
                    <div class="flex items-center space-x-4 mb-4">
                        <div id="structurePhotoPreview" class="w-20 h-20 bg-gradient-to-br from-blue-600 to-blue-800 rounded-full flex items-center justify-center text-white text-sm font-bold">
                            <!-- Photo preview will be populated -->
                        </div>
                        <div>
                            <input type="file" id="structurePhotoInput" accept="image/*" onchange="handleStructurePhotoUpload(event)" class="hidden">
                            <button type="button" onclick="document.getElementById('structurePhotoInput').click()" class="bg-blue-600 hover:bg-blue-700 text-white px-4 py-2 rounded-lg transition-colors mr-2">
                                <i class="fas fa-camera mr-2"></i>Pilih Foto
                            </button>
                            <button type="button" onclick="removeStructurePhoto()" class="bg-red-600 hover:bg-red-700 text-white px-4 py-2 rounded-lg transition-colors">
                                <i class="fas fa-trash mr-2"></i>Hapus
                            </button>
                        </div>
                    </div>
                    
                    <div class="border-t pt-4">
                        <p class="text-gray-600 text-sm mb-3">Atau pilih gaya default:</p>
                        <div class="grid grid-cols-4 gap-3">
                            <button type="button" onclick="selectStructurePhotoStyle('gradient')" class="structure-photo-style-btn p-3 border-2 border-gray-300 rounded-lg hover:border-blue-500 transition-colors">
                                <div class="w-12 h-12 bg-gradient-to-br from-blue-600 to-blue-800 rounded-full flex items-center justify-center text-white text-xs font-bold mx-auto mb-1">
                                    AB
                                </div>
                                <p class="text-xs text-gray-600">Gradient</p>
                            </button>
                            
                            <button type="button" onclick="selectStructurePhotoStyle('solid')" class="structure-photo-style-btn p-3 border-2 border-gray-300 rounded-lg hover:border-blue-500 transition-colors">
                                <div class="w-12 h-12 bg-blue-700 rounded-full flex items-center justify-center text-white text-xs font-bold mx-auto mb-1">
                                    AB
                                </div>
                                <p class="text-xs text-gray-600">Solid</p>
                            </button>
                            
                            <button type="button" onclick="selectStructurePhotoStyle('pattern')" class="structure-photo-style-btn p-3 border-2 border-gray-300 rounded-lg hover:border-blue-500 transition-colors">
                                <div class="w-12 h-12 bg-blue-600 rounded-full flex items-center justify-center text-white text-xs font-bold mx-auto mb-1 relative overflow-hidden">
                                    <div class="absolute inset-0 bg-blue-800 opacity-20" style="background-image: repeating-linear-gradient(45deg, transparent, transparent 2px, rgba(255,255,255,0.1) 2px, rgba(255,255,255,0.1) 4px);"></div>
                                    AB
                                </div>
                                <p class="text-xs text-gray-600">Pattern</p>
                            </button>
                            
                            <button type="button" onclick="selectStructurePhotoStyle('icon')" class="structure-photo-style-btn p-3 border-2 border-gray-300 rounded-lg hover:border-blue-500 transition-colors">
                                <div class="w-12 h-12 bg-blue-600 rounded-full flex items-center justify-center text-white mx-auto mb-1">
                                    <i class="fas fa-user text-lg"></i>
                                </div>
                                <p class="text-xs text-gray-600">Icon</p>
                            </button>
                        </div>
                    </div>
                </div>
                
                <div class="flex justify-between">
                    <button type="button" onclick="hideEditStructureItem()" class="bg-gray-500 hover:bg-gray-600 text-white px-4 py-2 rounded-lg transition-colors">
                        Batal
                    </button>
                    <button type="submit" class="bg-blue-600 hover:bg-blue-700 text-white px-6 py-2 rounded-lg transition-colors">
                        Simpan
                    </button>
                </div>
            </form>
        </div>
    </div>

    <!-- Footer -->
    <footer class="bg-gray-800 text-white mt-16">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-8">
            <div class="grid grid-cols-1 md:grid-cols-3 gap-8">
                <div>
                    <h3 class="text-lg font-semibold mb-4">BKPSDM Kabupaten Boalemo</h3>
                    <p class="text-gray-300">Jl. Trans Sulawesi No. 1, Tilamuta, Kabupaten Boalemo, Gorontalo 96319</p>
                </div>
                <div>
                    <h3 class="text-lg font-semibold mb-4">Kontak</h3>
                    <p class="text-gray-300">📞 (0435) 881234</p>
                    <p class="text-gray-300">📧 bkpsdm@boalemokab.go.id</p>
                </div>
                <div>
                    <h3 class="text-lg font-semibold mb-4">Jam Pelayanan</h3>
                    <p class="text-gray-300">Senin - Jumat: 08:00 - 16:00 WITA</p>
                    <p class="text-gray-300">Sabtu - Minggu: Tutup</p>
                </div>
            </div>
            <div class="border-t border-gray-700 mt-8 pt-8 text-center">
                <p class="text-gray-300">&copy; 2025 BKPSDM Kabupaten Boalemo. Semua hak dilindungi.</p>
            </div>
        </div>
    </footer>

    <script>
        // Global state
        let currentUser = null;
        let currentSection = 'beranda';
        let selectedPhotoStyle = 'gradient';
        let selectedNewsImage = null;
        let selectedAnnouncementImage = null;
        let selectedAnnouncementPDF = null;
        let currentEditingStructureItem = null;
        let selectedStructurePhoto = null;
        let selectedStructurePhotoStyle = 'gradient';
        let selectedGalleryImage = null;
        let currentViewingGallery = null;
        let currentViewingService = null;
        let currentServiceFilter = 'all';
        let currentSlide = 0;
        let currentHomepageSlide = 0;
        let slideInterval = null;
        let homepageSlideInterval = null;
        
        // Pegawai data
        let pegawaiData = {
            totalPegawai: 1247,
            asn: 856,
            pppk: 312,
            pppkParuhWaktu: 79
        };
        
        // System data
        let systemData = {
            activeYear: 2025
        };
        
        // User management data
        let usersData = [
            {
                id: 1,
                username: 'superadmin',
                password: 'super123',
                name: 'Super Administrator',
                role: 'superadmin',
                email: 'superadmin@boalemokab.go.id',
                createdDate: '2025-01-01'
            },
            {
                id: 2,
                username: 'admin',
                password: 'admin123',
                name: 'Administrator',
                role: 'admin',
                email: 'admin@boalemokab.go.id',
                createdDate: '2025-01-05'
            },
            {
                id: 3,
                username: 'user',
                password: 'user123',
                name: 'User Biasa',
                role: 'user',
                email: 'user@boalemokab.go.id',
                createdDate: '2025-01-10'
            }
        ];
        
        // Profile data
        let profileData = {
            visi: "Meningkatkan profesionalitas dan kompetensi Aparatur Sipil Negara (ASN). Misi utamanya adalah mewujudkan ASN yang memiliki pengetahuan dan keterampilan sesuai kompetensinya, meningkatkan kualitas manajemen kepegawaian, serta membangun tata kelola informasi kepegawaian yang lengkap dan akurat. ",
            misi: [
                "Mewujudkan sumber daya aparatur yang memiliki pengetahuan dan keterampilan sesuai dengan kompetensinya.",
                "Meningkatkan kualitas manajemen kepegawaian",
                "Mewujudkan tata kelola informasi kepegawaian yang lengkap dan akurat."
            ],
            photoStyle: 'gradient',
            customPhoto: null
        };

        let structureData = [
            {
                id: 1,
                position: "Kepala Badan",
                name: "Drs. H. Ahmad Syukur, M.Si",
                level: 1,
                parentId: null,
                photo: null,
                photoStyle: 'gradient'
            },
            {
                id: 2,
                position: "Sekretaris",
                name: "Hj. Siti Nurhaliza, S.Sos, M.AP",
                level: 2,
                parentId: 1,
                photo: null,
                photoStyle: 'solid'
            },
            {
                id: 3,
                position: "Bidang Formasi dan Informasi",
                name: "Drs. Muhammad Yusuf, M.Si",
                level: 2,
                parentId: 1,
                photo: null,
                photoStyle: 'pattern'
            },
            {
                id: 4,
                position: "Bidang Pengembangan SDM",
                name: "Dr. Hj. Fatimah Zahra, M.AP",
                level: 2,
                parentId: 1,
                photo: null,
                photoStyle: 'icon'
            },
            {
                id: 5,
                position: "Bidang Mutasi dan Promosi",
                name: "Drs. Abdul Rahman, M.Si",
                level: 2,
                parentId: 1,
                photo: null,
                photoStyle: 'gradient'
            }
        ];

        // Services data
        let servicesData = [
            {
                id: 1,
                name: "Pengurusan SK CPNS",
                category: "kepegawaian",
                type: "offline",
                time: "7-14 hari kerja",
                cost: "Gratis",
                description: "Layanan pengurusan Surat Keputusan (SK) CPNS untuk pegawai yang telah lulus seleksi CPNS dan memerlukan penerbitan SK pengangkatan.",
                requirements: [
                    "Fotokopi ijazah terakhir yang telah dilegalisir",
                    "Fotokopi transkrip nilai yang telah dilegalisir",
                    "Surat keterangan lulus dari BKN",
                    "Fotokopi KTP yang masih berlaku",
                    "Pas foto 4x6 sebanyak 6 lembar",
                    "Surat keterangan sehat dari dokter",
                    "Surat keterangan bebas narkoba"
                ],
                procedure: [
                    "Datang ke loket pelayanan BKPSDM dengan membawa berkas persyaratan",
                    "Mengisi formulir permohonan SK CPNS",
                    "Menyerahkan berkas persyaratan kepada petugas",
                    "Petugas melakukan verifikasi berkas",
                    "Menunggu proses penerbitan SK (7-14 hari kerja)",
                    "Mengambil SK CPNS yang telah selesai"
                ]
            },
            {
                id: 2,
                name: "Kenaikan Pangkat Reguler",
                category: "kepegawaian",
                type: "offline",
                time: "14-21 hari kerja",
                cost: "Gratis",
                description: "Layanan kenaikan pangkat reguler untuk ASN yang telah memenuhi syarat masa kerja dan persyaratan administratif lainnya.",
                requirements: [
                    "Surat pengantar dari atasan langsung",
                    "Fotokopi SK pangkat terakhir",
                    "Fotokopi SK jabatan (jika ada)",
                    "Daftar Penilaian Prestasi Kerja (DP3) 2 tahun terakhir",
                    "Surat keterangan tidak sedang menjalani hukuman disiplin",
                    "Fotokopi ijazah terakhir yang dilegalisir"
                ],
                procedure: [
                    "Mengajukan permohonan melalui atasan langsung",
                    "Menyiapkan berkas persyaratan lengkap",
                    "Menyerahkan berkas ke BKPSDM",
                    "Verifikasi berkas oleh tim verifikator",
                    "Proses penetapan kenaikan pangkat",
                    "Penerbitan SK kenaikan pangkat",
                    "Penyerahan SK kepada yang bersangkutan"
                ]
            },
            {
                id: 3,
                name: "Diklat Prajabatan CPNS",
                category: "diklat",
                type: "hybrid",
                time: "20 hari kerja",
                cost: "Gratis",
                description: "Program diklat prajabatan yang wajib diikuti oleh CPNS sebagai syarat pengangkatan menjadi PNS dengan sistem pembelajaran hybrid (online dan offline).",
                requirements: [
                    "SK CPNS yang masih berlaku",
                    "Fotokopi ijazah terakhir yang dilegalisir",
                    "Surat pengantar dari instansi",
                    "Surat keterangan sehat dari dokter",
                    "Pas foto 4x6 sebanyak 4 lembar",
                    "Laptop/smartphone untuk pembelajaran online"
                ],
                procedure: [
                    "Mendaftar melalui sistem informasi diklat online",
                    "Upload berkas persyaratan dalam format digital",
                    "Mengikuti pre-test online",
                    "Menghadiri pembukaan diklat secara offline",
                    "Mengikuti pembelajaran hybrid (online dan offline)",
                    "Mengerjakan tugas dan evaluasi",
                    "Mengikuti post-test dan ujian akhir",
                    "Menghadiri penutupan dan penyerahan sertifikat"
                ]
            },
            {
                id: 4,
                name: "Diklat Kepemimpinan",
                category: "diklat",
                type: "offline",
                time: "30 hari kerja",
                cost: "Gratis",
                description: "Program diklat kepemimpinan untuk ASN yang akan menduduki jabatan struktural atau fungsional tertentu guna meningkatkan kompetensi manajerial.",
                requirements: [
                    "SK pengangkatan dalam jabatan",
                    "Surat pengantar dari pimpinan instansi",
                    "Fotokopi ijazah S1 yang dilegalisir",
                    "Sertifikat diklat sebelumnya (jika ada)",
                    "Surat keterangan sehat dari dokter",
                    "Surat pernyataan kesediaan mengikuti diklat"
                ],
                procedure: [
                    "Mengajukan permohonan melalui instansi asal",
                    "Melengkapi berkas persyaratan",
                    "Mengikuti seleksi administrasi",
                    "Menghadiri pembukaan diklat",
                    "Mengikuti seluruh rangkaian pembelajaran",
                    "Menyusun dan mempresentasikan proyek perubahan",
                    "Mengikuti evaluasi akhir",
                    "Menerima sertifikat diklat kepemimpinan"
                ]
            },
            {
                id: 5,
                name: "Informasi Formasi CPNS",
                category: "informasi",
                type: "online",
                time: "Langsung",
                cost: "Gratis",
                description: "Layanan informasi mengenai formasi CPNS yang tersedia, persyaratan, dan jadwal pelaksanaan seleksi CPNS di lingkungan Pemerintah Kabupaten Boalemo.",
                requirements: [
                    "Akses internet",
                    "Browser web yang mendukung",
                    "Email aktif untuk berlangganan update"
                ],
                procedure: [
                    "Mengakses website resmi BKPSDM Boalemo",
                    "Membuka menu informasi CPNS",
                    "Membaca pengumuman formasi terbaru",
                    "Download dokumen formasi dan persyaratan",
                    "Mendaftar newsletter untuk update terbaru",
                    "Menghubungi call center jika ada pertanyaan"
                ]
            },
            {
                id: 6,
                name: "Konsultasi Kepegawaian",
                category: "konsultasi",
                type: "hybrid",
                time: "30 menit - 1 jam",
                cost: "Gratis",
                description: "Layanan konsultasi mengenai berbagai permasalahan kepegawaian, karir, dan pengembangan ASN yang dapat dilakukan secara langsung atau online.",
                requirements: [
                    "KTP atau identitas diri",
                    "SK kepegawaian (jika sudah PNS)",
                    "Dokumen terkait permasalahan yang dikonsultasikan",
                    "Formulir konsultasi yang telah diisi"
                ],
                procedure: [
                    "Membuat janji konsultasi melalui telepon atau online",
                    "Menyiapkan dokumen yang diperlukan",
                    "Datang sesuai jadwal yang telah ditentukan",
                    "Menyampaikan permasalahan kepada konselor",
                    "Mendiskusikan solusi dan alternatif penyelesaian",
                    "Menerima rekomendasi dan tindak lanjut",
                    "Follow up sesuai kesepakatan"
                ]
            },
            {
                id: 7,
                name: "Legalisir Dokumen Kepegawaian",
                category: "kepegawaian",
                type: "offline",
                time: "1-2 hari kerja",
                cost: "Gratis",
                description: "Layanan legalisir dokumen kepegawaian seperti SK, sertifikat, dan dokumen resmi lainnya yang dikeluarkan oleh BKPSDM.",
                requirements: [
                    "Dokumen asli yang akan dilegalisir",
                    "Fotokopi dokumen yang akan dilegalisir",
                    "KTP pemohon",
                    "Surat pengantar dari instansi (jika diperlukan)"
                ],
                procedure: [
                    "Datang ke loket pelayanan BKPSDM",
                    "Menyerahkan dokumen asli dan fotokopi",
                    "Mengisi formulir permohonan legalisir",
                    "Petugas melakukan verifikasi dokumen",
                    "Proses legalisir oleh pejabat berwenang",
                    "Pengambilan dokumen yang telah dilegalisir"
                ]
            },
            {
                id: 8,
                name: "Informasi Diklat dan Pelatihan",
                category: "informasi",
                type: "online",
                time: "Langsung",
                cost: "Gratis",
                description: "Layanan informasi mengenai jadwal, jenis, dan persyaratan berbagai diklat dan pelatihan yang tersedia untuk ASN di lingkungan Pemkab Boalemo.",
                requirements: [
                    "Akses internet",
                    "Email aktif",
                    "Nomor telepon yang dapat dihubungi"
                ],
                procedure: [
                    "Mengakses portal informasi diklat online",
                    "Browsing katalog diklat yang tersedia",
                    "Membaca detail persyaratan dan jadwal",
                    "Mendaftar untuk mendapat notifikasi",
                    "Download formulir pendaftaran jika berminat",
                    "Menghubungi bagian diklat untuk informasi lebih lanjut"
                ]
            }
        ];

        // Gallery data
        let galleryData = [
            {
                id: 1,
                title: "Pelatihan Kepemimpinan ASN Eselon III",
                category: "Kegiatan Diklat",
                description: "Kegiatan pelatihan kepemimpinan untuk ASN eselon III dalam rangka meningkatkan kapasitas manajerial dan kepemimpinan aparatur.",
                date: "2025-01-15",
                image: "data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='400' height='300' viewBox='0 0 400 300'%3E%3Crect width='400' height='300' fill='%234F46E5'/%3E%3Ctext x='200' y='150' font-family='Arial' font-size='16' fill='white' text-anchor='middle'%3EPelatihan Kepemimpinan%3C/text%3E%3C/svg%3E"
            },
            {
                id: 2,
                title: "Rapat Koordinasi Bulanan BKPSDM",
                category: "Rapat Koordinasi",
                description: "Rapat koordinasi rutin bulanan untuk evaluasi kinerja dan perencanaan program kerja BKPSDM Kabupaten Boalemo.",
                date: "2025-01-20",
                image: "data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='400' height='300' viewBox='0 0 400 300'%3E%3Crect width='400' height='300' fill='%2306B6D4'/%3E%3Ctext x='200' y='150' font-family='Arial' font-size='16' fill='white' text-anchor='middle'%3ERapat Koordinasi%3C/text%3E%3C/svg%3E"
            },
            {
                id: 3,
                title: "Pelayanan CPNS 2025",
                category: "Pelayanan Publik",
                description: "Kegiatan pelayanan pendaftaran dan verifikasi berkas CPNS 2025 di kantor BKPSDM Kabupaten Boalemo.",
                date: "2025-02-01",
                image: "data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='400' height='300' viewBox='0 0 400 300'%3E%3Crect width='400' height='300' fill='%2310B981'/%3E%3Ctext x='200' y='150' font-family='Arial' font-size='16' fill='white' text-anchor='middle'%3EPelayanan CPNS%3C/text%3E%3C/svg%3E"
            },
            {
                id: 4,
                title: "Upacara Hari Kemerdekaan RI",
                category: "Upacara",
                description: "Upacara peringatan Hari Kemerdekaan Republik Indonesia ke-80 di halaman kantor BKPSDM Kabupaten Boalemo.",
                date: "2024-08-17",
                image: "data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='400' height='300' viewBox='0 0 400 300'%3E%3Crect width='400' height='300' fill='%23DC2626'/%3E%3Ctext x='200' y='150' font-family='Arial' font-size='16' fill='white' text-anchor='middle'%3EUpacara 17 Agustus%3C/text%3E%3C/svg%3E"
            },
            {
                id: 5,
                title: "Sosialisasi Peraturan Kepegawaian Terbaru",
                category: "Sosialisasi",
                description: "Kegiatan sosialisasi peraturan kepegawaian terbaru kepada seluruh ASN di lingkungan Pemerintah Kabupaten Boalemo.",
                date: "2025-01-25",
                image: "data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='400' height='300' viewBox='0 0 400 300'%3E%3Crect width='400' height='300' fill='%23F59E0B'/%3E%3Ctext x='200' y='150' font-family='Arial' font-size='16' fill='white' text-anchor='middle'%3ESosialisasi Peraturan%3C/text%3E%3C/svg%3E"
            },
            {
                id: 6,
                title: "Kunjungan Kerja dari BKN Pusat",
                category: "Kunjungan",
                description: "Kunjungan kerja dari tim Badan Kepegawaian Negara (BKN) Pusat untuk monitoring dan evaluasi sistem kepegawaian.",
                date: "2025-02-05",
                image: "data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='400' height='300' viewBox='0 0 400 300'%3E%3Crect width='400' height='300' fill='%238B5CF6'/%3E%3Ctext x='200' y='150' font-family='Arial' font-size='16' fill='white' text-anchor='middle'%3EKunjungan BKN%3C/text%3E%3C/svg%3E"
            }
        ];
        
        // Sample data
        let newsData = [
            {
                id: 1,
                title: "Pembukaan Pendaftaran CPNS 2025 Kabupaten Boalemo",
                category: "Kepegawaian",
                content: "BKPSDM Kabupaten Boalemo mengumumkan pembukaan pendaftaran CPNS tahun 2025 dengan formasi 150 orang untuk berbagai jabatan. Pendaftaran dibuka mulai 15 Januari hingga 15 Februari 2025 melalui portal SSCASN.",
                date: "2025-01-15",
                author: "Admin BKPSDM",
                image: null
            },
            {
                id: 2,
                title: "Pelatihan Kepemimpinan untuk ASN Eselon III dan IV",
                category: "Pengembangan SDM",
                content: "Dalam rangka meningkatkan kapasitas kepemimpinan ASN, BKPSDM menyelenggarakan pelatihan kepemimpinan untuk pejabat eselon III dan IV. Pelatihan akan dilaksanakan selama 5 hari dengan narasumber dari LAN RI.",
                date: "2025-02-10",
                author: "Bidang Pengembangan",
                image: null
            },
            {
                id: 3,
                title: "Implementasi Sistem Informasi Kepegawaian Terintegrasi",
                category: "Pelayanan",
                content: "BKPSDM Boalemo meluncurkan sistem informasi kepegawaian terintegrasi untuk meningkatkan efisiensi pelayanan administrasi kepegawaian. Sistem ini memungkinkan ASN mengakses layanan secara online 24/7.",
                date: "2025-01-20",
                author: "Tim IT BKPSDM",
                image: null
            },
            {
                id: 4,
                title: "Workshop Digitalisasi Pelayanan Publik 2025",
                category: "Kegiatan",
                content: "BKPSDM mengadakan workshop digitalisasi pelayanan publik untuk seluruh ASN. Kegiatan ini bertujuan meningkatkan kemampuan ASN dalam memberikan pelayanan berbasis teknologi digital.",
                date: "2025-03-05",
                author: "Tim Pelatihan",
                image: null
            }
        ];

        let announcementData = [
            {
                id: 1,
                title: "Jadwal Pelaksanaan Tes CPNS 2025",
                category: "Seleksi",
                priority: "Tinggi",
                content: "Tes CPNS Kabupaten Boalemo akan dilaksanakan pada tanggal 20-25 Maret 2025 di berbagai lokasi. Peserta dimohon mempersiapkan diri dengan baik.",
                date: "2025-03-20",
                image: null,
                pdf: null,
                pdfName: null
            },
            {
                id: 2,
                title: "Libur Nasional Maulid Nabi Muhammad SAW",
                category: "Pengumuman Umum",
                priority: "Sedang",
                content: "Dalam rangka memperingati Maulid Nabi Muhammad SAW, kantor BKPSDM akan libur pada tanggal 5 September 2025.",
                date: "2025-09-05",
                image: null,
                pdf: null,
                pdfName: null
            }
        ];

        // Authentication functions
        function showLogin() {
            document.getElementById('loginModal').classList.remove('hidden');
        }

        function hideLogin() {
            document.getElementById('loginModal').classList.add('hidden');
            document.getElementById('username').value = '';
            document.getElementById('password').value = '';
        }

        function handleLogin(event) {
            event.preventDefault();
            const username = document.getElementById('username').value;
            const password = document.getElementById('password').value;

            // Find user in usersData
            const user = usersData.find(u => u.username === username && u.password === password);
            
            if (user) {
                currentUser = {
                    id: user.id,
                    username: user.username,
                    role: user.role,
                    name: user.name,
                    email: user.email
                };
                updateUIForUser();
                hideLogin();
                
                let roleText = '';
                switch(user.role) {
                    case 'superadmin':
                        roleText = 'Super Administrator';
                        break;
                    case 'admin':
                        roleText = 'Administrator';
                        break;
                    case 'user':
                        roleText = 'User';
                        break;
                }
                showNotification(`Login berhasil sebagai ${roleText}`, 'success');
            } else {
                showNotification('Username atau password salah!', 'error');
            }
        }

        function logout() {
            currentUser = null;
            updateUIForUser();
            showNotification('Logout berhasil', 'success');
        }

        function updateUIForUser() {
            const loginBtn = document.getElementById('loginBtn');
            const userProfileMenu = document.getElementById('userProfileMenu');
            const roleIndicator = document.getElementById('roleIndicator');
            const roleText = document.getElementById('roleText');
            const addNewsBtn = document.getElementById('addNewsBtn');
            const addAnnouncementBtn = document.getElementById('addAnnouncementBtn');
            const addGalleryBtn = document.getElementById('addGalleryBtn');
            const editProfileBtn = document.getElementById('editProfileBtn');
            const editPhotoBtn = document.getElementById('editPhotoBtn');
            const editStructureBtn = document.getElementById('editStructureBtn');
            const addUserBtn = document.getElementById('addUserBtn');
            const editPegawaiBtn = document.getElementById('editPegawaiBtn');
            const editYearBtn = document.getElementById('editYearBtn');
            
            // Navbar elements
            const navUsersLink = document.getElementById('navUsersLink');
            const navEditProfileBtn = document.getElementById('navEditProfileBtn');
            const navEditPhotoBtn = document.getElementById('navEditPhotoBtn');
            const navUsersBtn = document.getElementById('navUsersBtn');
            const userNameDisplay = document.getElementById('userNameDisplay');
            const dropdownUserName = document.getElementById('dropdownUserName');
            const dropdownUserRole = document.getElementById('dropdownUserRole');

            if (currentUser) {
                loginBtn.classList.add('hidden');
                userProfileMenu.classList.remove('hidden');
                roleIndicator.classList.remove('hidden');
                roleText.textContent = `Login sebagai: ${currentUser.name} (${currentUser.role.toUpperCase()})`;
                
                // Update profile menu display
                userNameDisplay.textContent = currentUser.name;
                dropdownUserName.textContent = currentUser.name;
                dropdownUserRole.textContent = currentUser.role.toUpperCase();

                if (currentUser.role === 'superadmin') {
                    // Super admin has all permissions including image upload
                    addNewsBtn.classList.remove('hidden');
                    addAnnouncementBtn.classList.remove('hidden');
                    if (addGalleryBtn) addGalleryBtn.classList.remove('hidden');
                    document.getElementById('addServiceBtn').classList.remove('hidden');
                    editProfileBtn.classList.remove('hidden');
                    editPhotoBtn.classList.remove('hidden');
                    editStructureBtn.classList.remove('hidden');
                    addUserBtn.classList.remove('hidden');
                    editPegawaiBtn.classList.remove('hidden');
                    editYearBtn.classList.remove('hidden');
                    navUsersLink.classList.remove('hidden');
                    navEditProfileBtn.classList.remove('hidden');
                    navEditPhotoBtn.classList.remove('hidden');
                    navUsersBtn.classList.remove('hidden');
                } else if (currentUser.role === 'admin') {
                    // Admin has content management permissions including image upload
                    addNewsBtn.classList.remove('hidden');
                    addAnnouncementBtn.classList.remove('hidden');
                    if (addGalleryBtn) addGalleryBtn.classList.remove('hidden');
                    document.getElementById('addServiceBtn').classList.remove('hidden');
                    editProfileBtn.classList.remove('hidden');
                    editPhotoBtn.classList.remove('hidden');
                    editStructureBtn.classList.remove('hidden');
                    editPegawaiBtn.classList.remove('hidden');
                    navEditProfileBtn.classList.remove('hidden');
                    navEditPhotoBtn.classList.remove('hidden');
                    // Hide user management and year edit for regular admin
                    addUserBtn.classList.add('hidden');
                    editYearBtn.classList.add('hidden');
                    navUsersLink.classList.add('hidden');
                    navUsersBtn.classList.add('hidden');
                } else {
                    // User has no management permissions
                    addNewsBtn.classList.add('hidden');
                    addAnnouncementBtn.classList.add('hidden');
                    if (addGalleryBtn) addGalleryBtn.classList.add('hidden');
                    document.getElementById('addServiceBtn').classList.add('hidden');
                    editProfileBtn.classList.add('hidden');
                    editPhotoBtn.classList.add('hidden');
                    editStructureBtn.classList.add('hidden');
                    addUserBtn.classList.add('hidden');
                    editPegawaiBtn.classList.add('hidden');
                    editYearBtn.classList.add('hidden');
                    navUsersLink.classList.add('hidden');
                    navEditProfileBtn.classList.add('hidden');
                    navEditPhotoBtn.classList.add('hidden');
                    navUsersBtn.classList.add('hidden');
                }
            } else {
                loginBtn.classList.remove('hidden');
                userProfileMenu.classList.add('hidden');
                roleIndicator.classList.add('hidden');
                addNewsBtn.classList.add('hidden');
                addAnnouncementBtn.classList.add('hidden');
                addGalleryBtn.classList.add('hidden');
                document.getElementById('addServiceBtn').classList.add('hidden');
                editProfileBtn.classList.add('hidden');
                editPhotoBtn.classList.add('hidden');
                editStructureBtn.classList.add('hidden');
                addUserBtn.classList.add('hidden');
                editPegawaiBtn.classList.add('hidden');
                editYearBtn.classList.add('hidden');
                navUsersLink.classList.add('hidden');
                navEditProfileBtn.classList.add('hidden');
                navEditPhotoBtn.classList.add('hidden');
                navUsersBtn.classList.add('hidden');
            }

            renderNews();
            renderAnnouncements();
            renderStructure();
            updateProfileDisplay();
            if (currentUser && currentUser.role === 'superadmin') {
                renderUsers();
            }
        }

        // Service functions
        function showAddService() {
            if (currentUser && (currentUser.role === 'admin' || currentUser.role === 'superadmin')) {
                document.getElementById('addServiceModal').classList.remove('hidden');
            } else {
                showNotification('Hanya admin dan super admin yang dapat menambah layanan', 'error');
            }
        }

        function hideAddService() {
            document.getElementById('addServiceModal').classList.add('hidden');
            document.getElementById('serviceName').value = '';
            document.getElementById('serviceCategory').value = '';
            document.getElementById('serviceType').value = '';
            document.getElementById('serviceTime').value = '';
            document.getElementById('serviceCost').value = '';
            document.getElementById('serviceRequirements').value = '';
            document.getElementById('serviceProcedure').value = '';
            document.getElementById('serviceDescription').value = '';
        }

        function handleAddService(event) {
            event.preventDefault();
            
            if (!currentUser || (currentUser.role !== 'admin' && currentUser.role !== 'superadmin')) {
                showNotification('Hanya admin dan super admin yang dapat menambah layanan', 'error');
                return;
            }

            const name = document.getElementById('serviceName').value;
            const category = document.getElementById('serviceCategory').value;
            const type = document.getElementById('serviceType').value;
            const time = document.getElementById('serviceTime').value;
            const cost = document.getElementById('serviceCost').value;
            const requirementsText = document.getElementById('serviceRequirements').value;
            const procedureText = document.getElementById('serviceProcedure').value;
            const description = document.getElementById('serviceDescription').value;

            const requirements = requirementsText.split('\n').filter(line => line.trim() !== '');
            const procedure = procedureText.split('\n').filter(line => line.trim() !== '');

            const newService = {
                id: servicesData.length + 1,
                name: name,
                category: category,
                type: type,
                time: time,
                cost: cost,
                description: description,
                requirements: requirements,
                procedure: procedure
            };

            servicesData.push(newService);
            renderServices();
            hideAddService();
            showNotification('Layanan berhasil ditambahkan!', 'success');
        }

        function filterServices(category) {
            currentServiceFilter = category;
            
            // Update filter button styles
            document.querySelectorAll('.service-filter-btn').forEach(btn => {
                btn.classList.remove('bg-indigo-600', 'text-white');
                btn.classList.add('bg-gray-200', 'text-gray-700', 'hover:bg-gray-300');
            });
            
            event.target.classList.remove('bg-gray-200', 'text-gray-700', 'hover:bg-gray-300');
            event.target.classList.add('bg-indigo-600', 'text-white');
            
            renderServices();
        }

        function renderServices() {
            const servicesGrid = document.getElementById('servicesGrid');
            servicesGrid.innerHTML = '';

            const filteredServices = currentServiceFilter === 'all' 
                ? servicesData 
                : servicesData.filter(service => service.category === currentServiceFilter);

            if (filteredServices.length === 0) {
                servicesGrid.innerHTML = '<div class="col-span-full text-center py-8 text-gray-500">Tidak ada layanan dalam kategori ini</div>';
                return;
            }

            filteredServices.forEach(service => {
                const serviceCard = document.createElement('div');
                serviceCard.className = 'bg-white rounded-lg shadow-md p-6 hover:shadow-lg transition-shadow cursor-pointer';
                serviceCard.onclick = () => showServiceDetail(service.id);
                
                const categoryColors = {
                    'kepegawaian': 'bg-blue-100 text-blue-800',
                    'diklat': 'bg-green-100 text-green-800',
                    'informasi': 'bg-yellow-100 text-yellow-800',
                    'konsultasi': 'bg-purple-100 text-purple-800'
                };

                const typeColors = {
                    'online': 'bg-green-100 text-green-800',
                    'offline': 'bg-red-100 text-red-800',
                    'hybrid': 'bg-blue-100 text-blue-800'
                };

                const categoryLabels = {
                    'kepegawaian': 'Kepegawaian',
                    'diklat': 'Diklat & Pengembangan',
                    'informasi': 'Informasi',
                    'konsultasi': 'Konsultasi'
                };

                const typeLabels = {
                    'online': 'Online',
                    'offline': 'Offline',
                    'hybrid': 'Online & Offline'
                };
                
                serviceCard.innerHTML = `
                    <div class="flex justify-between items-start mb-4">
                        <div class="flex flex-wrap gap-2">
                            <span class="text-xs font-semibold px-2.5 py-0.5 rounded ${categoryColors[service.category]}">
                                ${categoryLabels[service.category]}
                            </span>
                            <span class="text-xs font-semibold px-2.5 py-0.5 rounded ${typeColors[service.type]}">
                                ${typeLabels[service.type]}
                            </span>
                        </div>
                        ${currentUser && (currentUser.role === 'admin' || currentUser.role === 'superadmin') ? 
                            `<button onclick="event.stopPropagation(); deleteService(${service.id})" class="text-red-500 hover:text-red-700 transition-colors">
                                <i class="fas fa-trash text-sm"></i>
                            </button>` : ''
                        }
                    </div>
                    <h3 class="text-lg font-semibold text-gray-800 mb-3">${service.name}</h3>
                    <p class="text-gray-600 text-sm mb-4 line-clamp-3">${service.description}</p>
                    <div class="space-y-2 text-sm">
                        <div class="flex justify-between">
                            <span class="text-gray-500">Waktu:</span>
                            <span class="font-medium text-gray-800">${service.time}</span>
                        </div>
                        <div class="flex justify-between">
                            <span class="text-gray-500">Biaya:</span>
                            <span class="font-semibold ${service.cost.toLowerCase() === 'gratis' ? 'text-green-600' : 'text-blue-600'}">${service.cost}</span>
                        </div>
                    </div>
                    <div class="mt-4 pt-4 border-t border-gray-200">
                        <button class="w-full bg-indigo-600 hover:bg-indigo-700 text-white py-2 px-4 rounded-lg transition-colors text-sm font-medium">
                            Lihat Detail Layanan
                        </button>
                    </div>
                `;
                
                servicesGrid.appendChild(serviceCard);
            });
        }

        function showServiceDetail(id) {
            const service = servicesData.find(s => s.id === id);
            if (service) {
                currentViewingService = service;
                
                const categoryLabels = {
                    'kepegawaian': 'Kepegawaian',
                    'diklat': 'Diklat & Pengembangan',
                    'informasi': 'Informasi',
                    'konsultasi': 'Konsultasi'
                };

                const typeLabels = {
                    'online': 'Online',
                    'offline': 'Offline',
                    'hybrid': 'Online & Offline'
                };
                
                document.getElementById('serviceDetailTitle').textContent = service.name;
                document.getElementById('serviceDetailCategory').textContent = categoryLabels[service.category];
                document.getElementById('serviceDetailType').textContent = typeLabels[service.type];
                document.getElementById('serviceDetailTime').textContent = service.time;
                document.getElementById('serviceDetailCost').textContent = service.cost;
                document.getElementById('serviceDetailDescription').textContent = service.description;
                
                // Populate requirements
                const requirementsList = document.getElementById('serviceDetailRequirements');
                requirementsList.innerHTML = '';
                service.requirements.forEach(req => {
                    const li = document.createElement('li');
                    li.className = 'flex items-start';
                    li.innerHTML = `<i class="fas fa-check-circle text-green-500 mr-2 mt-0.5 flex-shrink-0"></i><span class="text-gray-700">${req}</span>`;
                    requirementsList.appendChild(li);
                });
                
                // Populate procedure
                const procedureList = document.getElementById('serviceDetailProcedure');
                procedureList.innerHTML = '';
                service.procedure.forEach((step, index) => {
                    const li = document.createElement('li');
                    li.className = 'flex items-start';
                    li.innerHTML = `<span class="bg-indigo-600 text-white text-xs font-bold rounded-full w-6 h-6 flex items-center justify-center mr-3 mt-0.5 flex-shrink-0">${index + 1}</span><span class="text-gray-700">${step}</span>`;
                    procedureList.appendChild(li);
                });
                
                // Show/hide edit and delete buttons for admin/superadmin
                const editBtn = document.getElementById('editServiceBtn');
                const deleteBtn = document.getElementById('deleteServiceBtn');
                if (currentUser && (currentUser.role === 'admin' || currentUser.role === 'superadmin')) {
                    editBtn.classList.remove('hidden');
                    deleteBtn.classList.remove('hidden');
                } else {
                    editBtn.classList.add('hidden');
                    deleteBtn.classList.add('hidden');
                }
                
                document.getElementById('serviceDetailModal').classList.remove('hidden');
            }
        }

        function hideServiceDetail() {
            document.getElementById('serviceDetailModal').classList.add('hidden');
            currentViewingService = null;
        }

        function deleteService(id) {
            if (!currentUser || (currentUser.role !== 'admin' && currentUser.role !== 'superadmin')) {
                showNotification('Hanya admin dan super admin yang dapat menghapus layanan', 'error');
                return;
            }

            if (confirm('Apakah Anda yakin ingin menghapus layanan ini?')) {
                servicesData = servicesData.filter(service => service.id !== id);
                renderServices();
                showNotification('Layanan berhasil dihapus!', 'success');
            }
        }

        function deleteCurrentService() {
            if (currentViewingService) {
                deleteService(currentViewingService.id);
                hideServiceDetail();
            }
        }

        function showEditService() {
            showNotification('Fitur edit layanan akan segera tersedia', 'info');
        }

        // Navigation functions
        function showSection(section) {
            // Hide all sections
            const sections = ['berandaSection', 'beritaSection', 'pengumumanSection', 'layananSection', 'galeriSection', 'profilSection', 'usersSection'];
            sections.forEach(s => {
                document.getElementById(s).classList.add('hidden');
            });

            // Show selected section
            document.getElementById(section + 'Section').classList.remove('hidden');
            document.getElementById(section + 'Section').classList.add('fade-in');
            
            currentSection = section;

            // Update stats if showing beranda
            if (section === 'beranda') {
                updateStats();
                renderLatestNews();
                initializeHomepageSlider();
            }
            
            // Render users if showing users section
            if (section === 'users' && currentUser && currentUser.role === 'superadmin') {
                renderUsers();
            }
            
            // Initialize gallery if showing gallery section
            if (section === 'galeri') {
                renderGallery();
                initializeSlider();
            }
            
            // Initialize services if showing services section
            if (section === 'layanan') {
                renderServices();
            }
        }

        // News functions
        function showAddNews() {
            if (currentUser && (currentUser.role === 'admin' || currentUser.role === 'superadmin')) {
                document.getElementById('addNewsModal').classList.remove('hidden');
            } else {
                showNotification('Hanya admin dan super admin yang dapat menambah berita', 'error');
            }
        }

        function hideAddNews() {
            document.getElementById('addNewsModal').classList.add('hidden');
            document.getElementById('newsTitle').value = '';
            document.getElementById('newsCategory').value = '';
            document.getElementById('newsDate').value = '';
            document.getElementById('newsContent').value = '';
            document.getElementById('newsImage').value = '';
            document.getElementById('newsImagePreview').classList.add('hidden');
            selectedNewsImage = null;
        }

        function handleNewsImageUpload(event) {
            const file = event.target.files[0];
            if (file) {
                // Check file size (max 5MB)
                if (file.size > 5 * 1024 * 1024) {
                    showNotification('Ukuran file terlalu besar. Maksimal 5MB.', 'error');
                    event.target.value = '';
                    return;
                }

                // Check file type
                if (!file.type.startsWith('image/')) {
                    showNotification('File harus berupa gambar.', 'error');
                    event.target.value = '';
                    return;
                }

                const reader = new FileReader();
                reader.onload = function(e) {
                    selectedNewsImage = e.target.result;
                    document.getElementById('newsImagePreviewImg').src = selectedNewsImage;
                    document.getElementById('newsImagePreview').classList.remove('hidden');
                };
                reader.readAsDataURL(file);
            }
        }

        function removeNewsImage() {
            selectedNewsImage = null;
            document.getElementById('newsImage').value = '';
            document.getElementById('newsImagePreview').classList.add('hidden');
        }

        function handleAddNews(event) {
            event.preventDefault();
            
            if (!currentUser || (currentUser.role !== 'admin' && currentUser.role !== 'superadmin')) {
                showNotification('Hanya admin dan super admin yang dapat menambah berita', 'error');
                return;
            }

            const title = document.getElementById('newsTitle').value;
            const category = document.getElementById('newsCategory').value;
            const newsDate = document.getElementById('newsDate').value;
            const content = document.getElementById('newsContent').value;

            const newNews = {
                id: newsData.length + 1,
                title: title,
                category: category,
                content: content,
                date: newsDate,
                author: currentUser.name,
                image: selectedNewsImage
            };

            newsData.unshift(newNews);
            renderNews();
            updateStats();
            hideAddNews();
            showNotification('Berita berhasil ditambahkan!', 'success');
        }

        function deleteNews(id) {
            if (!currentUser || (currentUser.role !== 'admin' && currentUser.role !== 'superadmin')) {
                showNotification('Hanya admin dan super admin yang dapat menghapus berita', 'error');
                return;
            }

            if (confirm('Apakah Anda yakin ingin menghapus berita ini?')) {
                newsData = newsData.filter(news => news.id !== id);
                renderNews();
                updateStats();
                showNotification('Berita berhasil dihapus!', 'success');
            }
        }

        function renderNews() {
            const newsGrid = document.getElementById('newsGrid');
            newsGrid.innerHTML = '';

            newsData.forEach(news => {
                const newsCard = document.createElement('div');
                newsCard.className = 'bg-white rounded-lg shadow-md overflow-hidden hover:shadow-lg transition-shadow';
                
                newsCard.innerHTML = `
                    ${news.image ? `<div class="h-48 overflow-hidden">
                        <img src="${news.image}" alt="${news.title}" class="w-full h-full object-cover">
                    </div>` : ''}
                    <div class="p-6">
                        <div class="flex justify-between items-start mb-3">
                            <span class="bg-blue-100 text-blue-800 text-xs font-semibold px-2.5 py-0.5 rounded">${news.category}</span>
                            ${currentUser && (currentUser.role === 'admin' || currentUser.role === 'superadmin') ? 
                                `<button onclick="deleteNews(${news.id})" class="text-red-500 hover:text-red-700 transition-colors">
                                    <i class="fas fa-trash"></i>
                                </button>` : ''
                            }
                        </div>
                        <h3 class="text-lg font-semibold text-gray-800 mb-2">${news.title}</h3>
                        <p class="text-gray-600 text-sm mb-4 line-clamp-3">${news.content.substring(0, 150)}...</p>
                        <div class="flex justify-between items-center text-sm text-gray-500">
                            <span><i class="fas fa-user mr-1"></i>${news.author}</span>
                            <span><i class="fas fa-calendar mr-1"></i>${formatDate(news.date)}</span>
                        </div>
                    </div>
                `;
                
                newsGrid.appendChild(newsCard);
            });
        }

        function renderLatestNews() {
            const latestNews = document.getElementById('latestNews');
            latestNews.innerHTML = '';

            const latest = newsData.slice(0, 3);
            latest.forEach(news => {
                const newsCard = document.createElement('div');
                newsCard.className = 'bg-gray-50 rounded-lg p-4 hover:bg-gray-100 transition-colors cursor-pointer';
                newsCard.onclick = () => showSection('berita');
                
                newsCard.innerHTML = `
                    <span class="bg-blue-100 text-blue-800 text-xs font-semibold px-2.5 py-0.5 rounded">${news.category}</span>
                    <h4 class="font-semibold text-gray-800 mt-2 mb-2">${news.title}</h4>
                    <p class="text-gray-600 text-sm mb-2">${news.content.substring(0, 100)}...</p>
                    <p class="text-xs text-gray-500">${formatDate(news.date)}</p>
                `;
                
                latestNews.appendChild(newsCard);
            });
        }

        // Announcement functions
        function showAddAnnouncement() {
            if (currentUser && (currentUser.role === 'admin' || currentUser.role === 'superadmin')) {
                document.getElementById('addAnnouncementModal').classList.remove('hidden');
            } else {
                showNotification('Hanya admin dan super admin yang dapat menambah pengumuman', 'error');
            }
        }

        function hideAddAnnouncement() {
            document.getElementById('addAnnouncementModal').classList.add('hidden');
            document.getElementById('announcementTitle').value = '';
            document.getElementById('announcementCategory').value = '';
            document.getElementById('announcementPriority').value = '';
            document.getElementById('announcementDate').value = '';
            document.getElementById('announcementContent').value = '';
            document.getElementById('announcementImage').value = '';
            document.getElementById('announcementImagePreview').classList.add('hidden');
            document.getElementById('announcementPDF').value = '';
            document.getElementById('announcementPDFPreview').classList.add('hidden');
            selectedAnnouncementImage = null;
            selectedAnnouncementPDF = null;
        }

        function handleAnnouncementImageUpload(event) {
            const file = event.target.files[0];
            if (file) {
                // Check file size (max 5MB)
                if (file.size > 5 * 1024 * 1024) {
                    showNotification('Ukuran file terlalu besar. Maksimal 5MB.', 'error');
                    event.target.value = '';
                    return;
                }

                // Check file type
                if (!file.type.startsWith('image/')) {
                    showNotification('File harus berupa gambar.', 'error');
                    event.target.value = '';
                    return;
                }

                const reader = new FileReader();
                reader.onload = function(e) {
                    selectedAnnouncementImage = e.target.result;
                    document.getElementById('announcementImagePreviewImg').src = selectedAnnouncementImage;
                    document.getElementById('announcementImagePreview').classList.remove('hidden');
                };
                reader.readAsDataURL(file);
            }
        }

        function removeAnnouncementImage() {
            selectedAnnouncementImage = null;
            document.getElementById('announcementImage').value = '';
            document.getElementById('announcementImagePreview').classList.add('hidden');
        }

        function handleAnnouncementPDFUpload(event) {
            const file = event.target.files[0];
            if (file) {
                // Check file size (max 10MB)
                if (file.size > 10 * 1024 * 1024) {
                    showNotification('Ukuran file terlalu besar. Maksimal 10MB.', 'error');
                    event.target.value = '';
                    return;
                }

                // Check file type
                if (file.type !== 'application/pdf') {
                    showNotification('File harus berupa PDF.', 'error');
                    event.target.value = '';
                    return;
                }

                const reader = new FileReader();
                reader.onload = function(e) {
                    selectedAnnouncementPDF = {
                        data: e.target.result,
                        name: file.name,
                        size: file.size
                    };
                    
                    document.getElementById('announcementPDFName').textContent = file.name;
                    document.getElementById('announcementPDFSize').textContent = formatFileSize(file.size);
                    document.getElementById('announcementPDFPreview').classList.remove('hidden');
                };
                reader.readAsDataURL(file);
            }
        }

        function removeAnnouncementPDF() {
            selectedAnnouncementPDF = null;
            document.getElementById('announcementPDF').value = '';
            document.getElementById('announcementPDFPreview').classList.add('hidden');
        }

        function formatFileSize(bytes) {
            if (bytes === 0) return '0 Bytes';
            const k = 1024;
            const sizes = ['Bytes', 'KB', 'MB', 'GB'];
            const i = Math.floor(Math.log(bytes) / Math.log(k));
            return parseFloat((bytes / Math.pow(k, i)).toFixed(2)) + ' ' + sizes[i];
        }

        function handleAddAnnouncement(event) {
            event.preventDefault();
            
            if (!currentUser || (currentUser.role !== 'admin' && currentUser.role !== 'superadmin')) {
                showNotification('Hanya admin dan super admin yang dapat menambah pengumuman', 'error');
                return;
            }

            const title = document.getElementById('announcementTitle').value;
            const category = document.getElementById('announcementCategory').value;
            const priority = document.getElementById('announcementPriority').value;
            const announcementDate = document.getElementById('announcementDate').value;
            const content = document.getElementById('announcementContent').value;

            const newAnnouncement = {
                id: announcementData.length + 1,
                title: title,
                category: category,
                priority: priority,
                content: content,
                date: announcementDate,
                image: selectedAnnouncementImage,
                pdf: selectedAnnouncementPDF ? selectedAnnouncementPDF.data : null,
                pdfName: selectedAnnouncementPDF ? selectedAnnouncementPDF.name : null
            };

            announcementData.unshift(newAnnouncement);
            renderAnnouncements();
            updateStats();
            hideAddAnnouncement();
            showNotification('Pengumuman berhasil ditambahkan!', 'success');
        }

        function deleteAnnouncement(id) {
            if (!currentUser || (currentUser.role !== 'admin' && currentUser.role !== 'superadmin')) {
                showNotification('Hanya admin dan super admin yang dapat menghapus pengumuman', 'error');
                return;
            }

            if (confirm('Apakah Anda yakin ingin menghapus pengumuman ini?')) {
                announcementData = announcementData.filter(announcement => announcement.id !== id);
                renderAnnouncements();
                updateStats();
                showNotification('Pengumuman berhasil dihapus!', 'success');
            }
        }

        function renderAnnouncements() {
            const announcementsList = document.getElementById('announcementsList');
            announcementsList.innerHTML = '';

            announcementData.forEach(announcement => {
                const priorityColors = {
                    'Tinggi': 'bg-red-100 text-red-800 border-red-200',
                    'Sedang': 'bg-yellow-100 text-yellow-800 border-yellow-200',
                    'Rendah': 'bg-green-100 text-green-800 border-green-200'
                };

                const announcementCard = document.createElement('div');
                announcementCard.className = `bg-white rounded-lg shadow-md p-6 border-l-4 ${priorityColors[announcement.priority] || 'border-gray-200'}`;
                
                announcementCard.innerHTML = `
                    <div class="flex justify-between items-start mb-3">
                        <div class="flex items-center space-x-3">
                            <span class="bg-blue-100 text-blue-800 text-xs font-semibold px-2.5 py-0.5 rounded">
                                <i class="fas fa-bullhorn mr-1"></i>${announcement.category || 'Pengumuman'}
                            </span>
                            <span class="text-xs font-semibold px-2.5 py-0.5 rounded ${priorityColors[announcement.priority]}">
                                ${announcement.priority}
                            </span>
                        </div>
                        ${currentUser && (currentUser.role === 'admin' || currentUser.role === 'superadmin') ? 
                            `<button onclick="deleteAnnouncement(${announcement.id})" class="text-red-500 hover:text-red-700 transition-colors">
                                <i class="fas fa-trash"></i>
                            </button>` : ''
                        }
                    </div>
                    <h3 class="text-xl font-semibold text-gray-800 mb-3">${announcement.title}</h3>
                    ${announcement.image ? `<div class="mb-4">
                        <img src="${announcement.image}" alt="${announcement.title}" class="w-full max-w-md h-48 object-cover rounded-lg">
                    </div>` : ''}
                    <p class="text-gray-600 mb-4">${announcement.content}</p>
                    ${announcement.pdf ? `<div class="mb-4 p-3 bg-gray-50 rounded-lg border">
                        <div class="flex items-center justify-between">
                            <div class="flex items-center">
                                <i class="fas fa-file-pdf text-red-500 text-2xl mr-3"></i>
                                <div>
                                    <p class="text-sm font-medium text-gray-800">${announcement.pdfName}</p>
                                    <p class="text-xs text-gray-500">Dokumen PDF</p>
                                </div>
                            </div>
                            <a href="${announcement.pdf}" download="${announcement.pdfName}" class="bg-blue-600 hover:bg-blue-700 text-white px-3 py-1 rounded text-sm transition-colors">
                                <i class="fas fa-download mr-1"></i>Unduh
                            </a>
                        </div>
                    </div>` : ''}
                    <p class="text-sm text-gray-500">
                        <i class="fas fa-calendar mr-1"></i>Tanggal: ${formatDate(announcement.date)}
                    </p>
                `;
                
                announcementsList.appendChild(announcementCard);
            });
        }

        // Utility functions
        function formatDate(dateString) {
            const options = { year: 'numeric', month: 'long', day: 'numeric' };
            return new Date(dateString).toLocaleDateString('id-ID', options);
        }

        function updateStats() {
            document.getElementById('totalBerita').textContent = newsData.length;
            document.getElementById('totalPengumuman').textContent = announcementData.length;
            document.getElementById('totalPegawai').textContent = pegawaiData.totalPegawai.toLocaleString('id-ID');
            document.getElementById('activeYear').textContent = systemData.activeYear;
        }

        function showNotification(message, type) {
            const notification = document.createElement('div');
            notification.className = `fixed top-4 right-4 z-50 p-4 rounded-lg shadow-lg transition-all duration-300 ${
                type === 'success' ? 'bg-green-500 text-white' : 'bg-red-500 text-white'
            }`;
            notification.innerHTML = `
                <div class="flex items-center">
                    <i class="fas ${type === 'success' ? 'fa-check-circle' : 'fa-exclamation-circle'} mr-2"></i>
                    ${message}
                </div>
            `;
            
            document.body.appendChild(notification);
            
            setTimeout(() => {
                notification.style.transform = 'translateX(100%)';
                setTimeout(() => {
                    document.body.removeChild(notification);
                }, 300);
            }, 3000);
        }

        // Photo editing functions
        function showEditPhoto() {
            if (currentUser && (currentUser.role === 'admin' || currentUser.role === 'superadmin')) {
                document.getElementById('editPhotoModal').classList.remove('hidden');
                selectedPhotoStyle = profileData.photoStyle;
                updatePhotoPreview();
            } else {
                showNotification('Hanya admin dan super admin yang dapat mengedit foto profil', 'error');
            }
        }

        function hideEditPhoto() {
            document.getElementById('editPhotoModal').classList.add('hidden');
            // Reset file input
            document.getElementById('photoFileInput').value = '';
        }

        function handlePhotoUpload(event) {
            const file = event.target.files[0];
            if (file) {
                // Check file size (max 5MB)
                if (file.size > 5 * 1024 * 1024) {
                    showNotification('Ukuran file terlalu besar. Maksimal 5MB.', 'error');
                    return;
                }

                // Check file type
                if (!file.type.startsWith('image/')) {
                    showNotification('File harus berupa gambar.', 'error');
                    return;
                }

                const reader = new FileReader();
                reader.onload = function(e) {
                    selectedPhotoStyle = 'custom';
                    profileData.customPhoto = e.target.result;
                    updatePhotoPreview();
                    
                    // Clear style button selections
                    document.querySelectorAll('.photo-style-btn').forEach(btn => {
                        btn.classList.remove('border-blue-500', 'bg-blue-50');
                        btn.classList.add('border-gray-300');
                    });
                };
                reader.readAsDataURL(file);
            }
        }

        function selectPhotoStyle(style) {
            selectedPhotoStyle = style;
            updatePhotoPreview();
            
            // Update button selection
            document.querySelectorAll('.photo-style-btn').forEach(btn => {
                btn.classList.remove('border-blue-500', 'bg-blue-50');
                btn.classList.add('border-gray-300');
            });
            event.target.closest('.photo-style-btn').classList.add('border-blue-500', 'bg-blue-50');
        }

        function updatePhotoPreview() {
            const preview = document.getElementById('previewPhoto');
            
            let photoHTML = '';
            
            switch(selectedPhotoStyle) {
                case 'custom':
                    if (profileData.customPhoto) {
                        photoHTML = `<img src="${profileData.customPhoto}" alt="Foto Profil" class="w-full h-full object-cover rounded-full">`;
                    } else {
                        photoHTML = '<div class="w-full h-full bg-gradient-to-br from-blue-600 to-blue-800 rounded-full flex items-center justify-center text-white text-4xl font-bold">BKPSDM</div>';
                    }
                    break;
                case 'gradient':
                    photoHTML = '<div class="w-full h-full bg-gradient-to-br from-blue-600 to-blue-800 rounded-full flex items-center justify-center text-white text-4xl font-bold">BKPSDM</div>';
                    break;
                case 'solid':
                    photoHTML = '<div class="w-full h-full bg-blue-700 rounded-full flex items-center justify-center text-white text-4xl font-bold">BKPSDM</div>';
                    break;
                case 'pattern':
                    photoHTML = '<div class="w-full h-full bg-blue-600 rounded-full flex items-center justify-center text-white text-4xl font-bold relative overflow-hidden"><div class="absolute inset-0 bg-blue-800 opacity-20" style="background-image: repeating-linear-gradient(45deg, transparent, transparent 2px, rgba(255,255,255,0.1) 2px, rgba(255,255,255,0.1) 4px);"></div>BKPSDM</div>';
                    break;
                case 'icon':
                    photoHTML = '<div class="w-full h-full bg-blue-600 rounded-full flex items-center justify-center text-white"><i class="fas fa-building text-4xl"></i></div>';
                    break;
            }
            
            preview.innerHTML = photoHTML;
        }

        function savePhotoStyle() {
            profileData.photoStyle = selectedPhotoStyle;
            updateProfileDisplay();
            hideEditPhoto();
            showNotification('Foto profil berhasil diperbarui!', 'success');
        }

        function updateProfileDisplay() {
            const mainPhoto = document.getElementById('profilePhoto');
            
            switch(profileData.photoStyle) {
                case 'custom':
                    if (profileData.customPhoto) {
                        mainPhoto.className = 'w-32 h-32 rounded-full shadow-lg overflow-hidden';
                        mainPhoto.innerHTML = `<img src="${profileData.customPhoto}" alt="Foto Profil" class="w-full h-full object-cover">`;
                    } else {
                        mainPhoto.className = 'w-32 h-32 bg-gradient-to-br from-blue-600 to-blue-800 rounded-full flex items-center justify-center text-white text-4xl font-bold shadow-lg';
                        mainPhoto.innerHTML = 'BKPSDM';
                    }
                    break;
                case 'gradient':
                    mainPhoto.className = 'w-32 h-32 bg-gradient-to-br from-blue-600 to-blue-800 rounded-full flex items-center justify-center text-white text-4xl font-bold shadow-lg';
                    mainPhoto.innerHTML = 'BKPSDM';
                    break;
                case 'solid':
                    mainPhoto.className = 'w-32 h-32 bg-blue-700 rounded-full flex items-center justify-center text-white text-4xl font-bold shadow-lg';
                    mainPhoto.innerHTML = 'BKPSDM';
                    break;
                case 'pattern':
                    mainPhoto.className = 'w-32 h-32 bg-blue-600 rounded-full flex items-center justify-center text-white text-4xl font-bold shadow-lg relative overflow-hidden';
                    mainPhoto.innerHTML = '<div class="absolute inset-0 bg-blue-800 opacity-20" style="background-image: repeating-linear-gradient(45deg, transparent, transparent 2px, rgba(255,255,255,0.1) 2px, rgba(255,255,255,0.1) 4px);"></div>BKPSDM';
                    break;
                case 'icon':
                    mainPhoto.className = 'w-32 h-32 bg-blue-600 rounded-full flex items-center justify-center text-white shadow-lg';
                    mainPhoto.innerHTML = '<i class="fas fa-building text-4xl"></i>';
                    break;
            }
            
            // Update visi and misi display
            document.getElementById('visiText').textContent = profileData.visi;
            
            const misiList = document.getElementById('misiList');
            misiList.innerHTML = '';
            profileData.misi.forEach(misi => {
                const li = document.createElement('li');
                li.className = 'flex items-start';
                li.innerHTML = `<i class="fas fa-check text-green-600 mr-3 mt-1"></i>${misi}`;
                misiList.appendChild(li);
            });
        }

        // Profile editing functions
        function showEditProfile() {
            if (currentUser && (currentUser.role === 'admin' || currentUser.role === 'superadmin')) {
                document.getElementById('editProfileModal').classList.remove('hidden');
                document.getElementById('editVisi').value = profileData.visi;
                document.getElementById('editMisi').value = profileData.misi.join('\n');
            } else {
                showNotification('Hanya admin dan super admin yang dapat mengedit profil', 'error');
            }
        }

        function hideEditProfile() {
            document.getElementById('editProfileModal').classList.add('hidden');
        }

        function handleEditProfile(event) {
            event.preventDefault();
            
            if (!currentUser || (currentUser.role !== 'admin' && currentUser.role !== 'superadmin')) {
                showNotification('Hanya admin dan super admin yang dapat mengedit profil', 'error');
                return;
            }

            const visi = document.getElementById('editVisi').value;
            const misiText = document.getElementById('editMisi').value;
            const misiArray = misiText.split('\n').filter(line => line.trim() !== '');

            profileData.visi = visi;
            profileData.misi = misiArray;

            updateProfileDisplay();
            hideEditProfile();
            showNotification('Profil organisasi berhasil diperbarui!', 'success');
        }

        // Structure editing functions
        function showEditStructure() {
            if (currentUser && (currentUser.role === 'admin' || currentUser.role === 'superadmin')) {
                document.getElementById('editStructureModal').classList.remove('hidden');
                renderStructureEditor();
            } else {
                showNotification('Hanya admin dan super admin yang dapat mengedit struktur organisasi', 'error');
            }
        }

        function hideEditStructure() {
            document.getElementById('editStructureModal').classList.add('hidden');
        }

        function renderStructureEditor() {
            const editor = document.getElementById('structureEditor');
            editor.innerHTML = '';

            // Group by level
            const level1Items = structureData.filter(item => item.level === 1);
            const level2Items = structureData.filter(item => item.level === 2);

            // Level 1 section
            if (level1Items.length > 0) {
                const level1Section = document.createElement('div');
                level1Section.className = 'mb-6';
                level1Section.innerHTML = '<h3 class="text-lg font-semibold text-gray-800 mb-4">Kepala Badan</h3>';
                
                level1Items.forEach(item => {
                    const itemCard = createStructureEditorCard(item);
                    level1Section.appendChild(itemCard);
                });
                
                editor.appendChild(level1Section);
            }

            // Level 2 section
            if (level2Items.length > 0) {
                const level2Section = document.createElement('div');
                level2Section.className = 'mb-6';
                level2Section.innerHTML = '<h3 class="text-lg font-semibold text-gray-800 mb-4">Bidang-bidang</h3>';
                
                level2Items.forEach(item => {
                    const itemCard = createStructureEditorCard(item);
                    level2Section.appendChild(itemCard);
                });
                
                editor.appendChild(level2Section);
            }
        }

        function createStructureEditorCard(item) {
            const card = document.createElement('div');
            card.className = 'border border-gray-300 rounded-lg p-4 mb-4 bg-gray-50';
            
            const photoElement = createStructurePhoto(item);
            
            card.innerHTML = `
                <div class="flex items-start space-x-4">
                    <div class="flex-shrink-0">
                        ${photoElement}
                    </div>
                    <div class="flex-1">
                        <div class="flex justify-between items-start mb-3">
                            <h4 class="font-semibold text-gray-800">${item.position}</h4>
                            <div class="flex space-x-2">
                                <button onclick="showEditStructureItem(${item.id})" class="text-blue-600 hover:text-blue-800 transition-colors">
                                    <i class="fas fa-edit"></i>
                                </button>
                                ${item.level !== 1 ? `<button onclick="removeStructureItem(${item.id})" class="text-red-500 hover:text-red-700 transition-colors">
                                    <i class="fas fa-trash"></i>
                                </button>` : ''}
                            </div>
                        </div>
                        <p class="text-gray-600">${item.name}</p>
                    </div>
                </div>
            `;
            
            return card;
        }

        function showEditStructureItem(id) {
            const item = structureData.find(item => item.id === id);
            if (item) {
                currentEditingStructureItem = item;
                selectedStructurePhoto = item.photo;
                selectedStructurePhotoStyle = item.photoStyle || 'gradient';
                
                document.getElementById('editStructureItemId').value = item.id;
                document.getElementById('editStructurePosition').value = item.position;
                document.getElementById('editStructureName').value = item.name;
                
                updateStructurePhotoPreview();
                document.getElementById('editStructureItemModal').classList.remove('hidden');
            }
        }

        function hideEditStructureItem() {
            document.getElementById('editStructureItemModal').classList.add('hidden');
            currentEditingStructureItem = null;
            selectedStructurePhoto = null;
            selectedStructurePhotoStyle = 'gradient';
        }

        function handleStructurePhotoUpload(event) {
            const file = event.target.files[0];
            if (file) {
                // Check file size (max 5MB)
                if (file.size > 5 * 1024 * 1024) {
                    showNotification('Ukuran file terlalu besar. Maksimal 5MB.', 'error');
                    event.target.value = '';
                    return;
                }

                // Check file type
                if (!file.type.startsWith('image/')) {
                    showNotification('File harus berupa gambar.', 'error');
                    event.target.value = '';
                    return;
                }

                const reader = new FileReader();
                reader.onload = function(e) {
                    selectedStructurePhoto = e.target.result;
                    selectedStructurePhotoStyle = 'custom';
                    updateStructurePhotoPreview();
                };
                reader.readAsDataURL(file);
            }
        }

        function removeStructurePhoto() {
            selectedStructurePhoto = null;
            selectedStructurePhotoStyle = 'gradient';
            document.getElementById('structurePhotoInput').value = '';
            updateStructurePhotoPreview();
        }

        function selectStructurePhotoStyle(style) {
            selectedStructurePhotoStyle = style;
            selectedStructurePhoto = null;
            updateStructurePhotoPreview();
            
            // Update button selection
            document.querySelectorAll('.structure-photo-style-btn').forEach(btn => {
                btn.classList.remove('border-blue-500', 'bg-blue-50');
                btn.classList.add('border-gray-300');
            });
            event.target.closest('.structure-photo-style-btn').classList.add('border-blue-500', 'bg-blue-50');
        }

        function updateStructurePhotoPreview() {
            const preview = document.getElementById('structurePhotoPreview');
            if (!currentEditingStructureItem) return;
            
            const initials = currentEditingStructureItem.name.split(' ').map(word => word.charAt(0)).join('').substring(0, 2).toUpperCase();
            
            if (selectedStructurePhoto) {
                preview.className = 'w-20 h-20 rounded-full overflow-hidden shadow-md';
                preview.innerHTML = `<img src="${selectedStructurePhoto}" alt="Preview" class="w-full h-full object-cover">`;
                return;
            }
            
            switch(selectedStructurePhotoStyle) {
                case 'gradient':
                    preview.className = 'w-20 h-20 bg-gradient-to-br from-blue-600 to-blue-800 rounded-full flex items-center justify-center text-white text-sm font-bold shadow-md';
                    preview.innerHTML = initials;
                    break;
                case 'solid':
                    preview.className = 'w-20 h-20 bg-blue-700 rounded-full flex items-center justify-center text-white text-sm font-bold shadow-md';
                    preview.innerHTML = initials;
                    break;
                case 'pattern':
                    preview.className = 'w-20 h-20 bg-blue-600 rounded-full flex items-center justify-center text-white text-sm font-bold shadow-md relative overflow-hidden';
                    preview.innerHTML = `<div class="absolute inset-0 bg-blue-800 opacity-20" style="background-image: repeating-linear-gradient(45deg, transparent, transparent 2px, rgba(255,255,255,0.1) 2px, rgba(255,255,255,0.1) 4px);"></div>${initials}`;
                    break;
                case 'icon':
                    preview.className = 'w-20 h-20 bg-blue-600 rounded-full flex items-center justify-center text-white shadow-md';
                    preview.innerHTML = '<i class="fas fa-user text-xl"></i>';
                    break;
            }
        }

        function handleEditStructureItem(event) {
            event.preventDefault();
            
            if (!currentUser || (currentUser.role !== 'admin' && currentUser.role !== 'superadmin')) {
                showNotification('Hanya admin dan super admin yang dapat mengedit struktur organisasi', 'error');
                return;
            }

            const id = parseInt(document.getElementById('editStructureItemId').value);
            const position = document.getElementById('editStructurePosition').value;
            const name = document.getElementById('editStructureName').value;

            const itemIndex = structureData.findIndex(item => item.id === id);
            if (itemIndex !== -1) {
                structureData[itemIndex].position = position;
                structureData[itemIndex].name = name;
                structureData[itemIndex].photo = selectedStructurePhoto;
                structureData[itemIndex].photoStyle = selectedStructurePhotoStyle;

                renderStructure();
                renderStructureEditor();
                hideEditStructureItem();
                showNotification('Jabatan berhasil diperbarui!', 'success');
            }
        }

        function addStructureItem() {
            const newId = Math.max(...structureData.map(item => item.id)) + 1;
            structureData.push({
                id: newId,
                position: "Bidang Baru",
                name: "Nama Pejabat Baru",
                level: 2,
                parentId: 1,
                photo: null,
                photoStyle: 'gradient'
            });
            renderStructureEditor();
        }

        function removeStructureItem(id) {
            const item = structureData.find(item => item.id === id);
            if (item && item.level === 1) {
                showNotification('Kepala Badan tidak dapat dihapus!', 'error');
                return;
            }
            
            if (confirm('Apakah Anda yakin ingin menghapus jabatan ini?')) {
                structureData = structureData.filter(item => item.id !== id);
                renderStructureEditor();
                renderStructure();
            }
        }

        function saveStructure() {
            renderStructure();
            hideEditStructure();
            showNotification('Struktur organisasi berhasil diperbarui!', 'success');
        }

        function renderStructure() {
            const structureChart = document.getElementById('structureChart');
            structureChart.innerHTML = '';

            // Create organizational chart
            const chartContainer = document.createElement('div');
            chartContainer.className = 'min-w-full';

            // Level 1 (Kepala Badan)
            const level1Items = structureData.filter(item => item.level === 1);
            if (level1Items.length > 0) {
                const level1Container = document.createElement('div');
                level1Container.className = 'flex justify-center mb-8';
                
                level1Items.forEach(item => {
                    const itemElement = createStructureItem(item, true);
                    level1Container.appendChild(itemElement);
                });
                
                chartContainer.appendChild(level1Container);
            }

            // Connection line
            const connectionLine = document.createElement('div');
            connectionLine.className = 'flex justify-center mb-4';
            connectionLine.innerHTML = '<div class="w-px h-8 bg-gray-400"></div>';
            chartContainer.appendChild(connectionLine);

            // Level 2 (Bidang-bidang)
            const level2Items = structureData.filter(item => item.level === 2);
            if (level2Items.length > 0) {
                // Horizontal line
                const horizontalLine = document.createElement('div');
                horizontalLine.className = 'flex justify-center mb-4';
                horizontalLine.innerHTML = `<div class="h-px bg-gray-400" style="width: ${Math.min(level2Items.length * 200, 800)}px;"></div>`;
                chartContainer.appendChild(horizontalLine);

                // Vertical lines
                const verticalLines = document.createElement('div');
                verticalLines.className = 'flex justify-center mb-4';
                const lineContainer = document.createElement('div');
                lineContainer.className = 'flex justify-between';
                lineContainer.style.width = `${Math.min(level2Items.length * 200, 800)}px`;
                
                level2Items.forEach(() => {
                    const line = document.createElement('div');
                    line.className = 'w-px h-8 bg-gray-400';
                    lineContainer.appendChild(line);
                });
                
                verticalLines.appendChild(lineContainer);
                chartContainer.appendChild(verticalLines);

                // Level 2 items
                const level2Container = document.createElement('div');
                level2Container.className = 'flex justify-center flex-wrap gap-4';
                
                level2Items.forEach(item => {
                    const itemElement = createStructureItem(item, false);
                    level2Container.appendChild(itemElement);
                });
                
                chartContainer.appendChild(level2Container);
            }

            structureChart.appendChild(chartContainer);
        }

        function createStructureItem(item, isHead = false) {
            const itemDiv = document.createElement('div');
            itemDiv.className = `bg-white rounded-lg shadow-md p-4 text-center ${isHead ? 'border-2 border-blue-500' : 'border border-gray-200'} hover:shadow-lg transition-shadow relative`;
            itemDiv.style.minWidth = '180px';
            
            // Create photo element
            const photoElement = createStructurePhoto(item);
            
            itemDiv.innerHTML = `
                ${currentUser && (currentUser.role === 'admin' || currentUser.role === 'superadmin') ? 
                    `<button onclick="showEditStructureItem(${item.id})" class="absolute top-2 right-2 text-blue-600 hover:text-blue-800 transition-colors">
                        <i class="fas fa-edit text-sm"></i>
                    </button>` : ''
                }
                <div class="mb-3 flex justify-center">
                    ${photoElement}
                </div>
                <h3 class="font-semibold text-gray-800 text-sm mb-1">${item.position}</h3>
                <p class="text-gray-600 text-xs">${item.name}</p>
            `;
            
            return itemDiv;
        }

        function createStructurePhoto(item) {
            const initials = item.name.split(' ').map(word => word.charAt(0)).join('').substring(0, 2).toUpperCase();
            
            if (item.photo) {
                return `<div class="w-16 h-16 rounded-full overflow-hidden shadow-md">
                    <img src="${item.photo}" alt="${item.name}" class="w-full h-full object-cover">
                </div>`;
            }
            
            switch(item.photoStyle) {
                case 'gradient':
                    return `<div class="w-16 h-16 bg-gradient-to-br from-blue-600 to-blue-800 rounded-full flex items-center justify-center text-white text-sm font-bold shadow-md">
                        ${initials}
                    </div>`;
                case 'solid':
                    return `<div class="w-16 h-16 bg-blue-700 rounded-full flex items-center justify-center text-white text-sm font-bold shadow-md">
                        ${initials}
                    </div>`;
                case 'pattern':
                    return `<div class="w-16 h-16 bg-blue-600 rounded-full flex items-center justify-center text-white text-sm font-bold shadow-md relative overflow-hidden">
                        <div class="absolute inset-0 bg-blue-800 opacity-20" style="background-image: repeating-linear-gradient(45deg, transparent, transparent 2px, rgba(255,255,255,0.1) 2px, rgba(255,255,255,0.1) 4px);"></div>
                        ${initials}
                    </div>`;
                case 'icon':
                    return `<div class="w-16 h-16 bg-blue-600 rounded-full flex items-center justify-center text-white shadow-md">
                        <i class="fas fa-user text-xl"></i>
                    </div>`;
                default:
                    return `<div class="w-16 h-16 bg-gradient-to-br from-blue-600 to-blue-800 rounded-full flex items-center justify-center text-white text-sm font-bold shadow-md">
                        ${initials}
                    </div>`;
            }
        }

        // Pegawai editing functions
        function showEditPegawai() {
            if (currentUser && (currentUser.role === 'admin' || currentUser.role === 'superadmin')) {
                document.getElementById('editPegawaiModal').classList.remove('hidden');
                document.getElementById('editASNCount').value = pegawaiData.asn;
                document.getElementById('editPPPKCount').value = pegawaiData.pppk;
                document.getElementById('editPPPKParuhWaktuCount').value = pegawaiData.pppkParuhWaktu;
                updateTotalPegawaiPreview();
                
                // Add event listeners for real-time calculation
                document.getElementById('editASNCount').addEventListener('input', updateTotalPegawaiPreview);
                document.getElementById('editPPPKCount').addEventListener('input', updateTotalPegawaiPreview);
                document.getElementById('editPPPKParuhWaktuCount').addEventListener('input', updateTotalPegawaiPreview);
            } else {
                showNotification('Hanya admin yang dapat mengedit data pegawai', 'error');
            }
        }

        function hideEditPegawai() {
            document.getElementById('editPegawaiModal').classList.add('hidden');
            
            // Remove event listeners
            document.getElementById('editASNCount').removeEventListener('input', updateTotalPegawaiPreview);
            document.getElementById('editPPPKCount').removeEventListener('input', updateTotalPegawaiPreview);
            document.getElementById('editPPPKParuhWaktuCount').removeEventListener('input', updateTotalPegawaiPreview);
        }

        function updateTotalPegawaiPreview() {
            const asn = parseInt(document.getElementById('editASNCount').value) || 0;
            const pppk = parseInt(document.getElementById('editPPPKCount').value) || 0;
            const pppkParuhWaktu = parseInt(document.getElementById('editPPPKParuhWaktuCount').value) || 0;
            const total = asn + pppk + pppkParuhWaktu;
            
            document.getElementById('totalPegawaiPreview').textContent = total.toLocaleString('id-ID');
        }

        function handleEditPegawai(event) {
            event.preventDefault();
            
            if (!currentUser || (currentUser.role !== 'admin' && currentUser.role !== 'superadmin')) {
                showNotification('Hanya admin yang dapat mengedit data pegawai', 'error');
                return;
            }

            const asn = parseInt(document.getElementById('editASNCount').value);
            const pppk = parseInt(document.getElementById('editPPPKCount').value);
            const pppkParuhWaktu = parseInt(document.getElementById('editPPPKParuhWaktuCount').value);
            
            if (asn < 0 || pppk < 0 || pppkParuhWaktu < 0) {
                showNotification('Jumlah pegawai tidak boleh negatif', 'error');
                return;
            }

            pegawaiData.asn = asn;
            pegawaiData.pppk = pppk;
            pegawaiData.pppkParuhWaktu = pppkParuhWaktu;
            pegawaiData.totalPegawai = asn + pppk + pppkParuhWaktu;
            
            updateStats();
            hideEditPegawai();
            showNotification('Data pegawai berhasil diperbarui!', 'success');
        }

        // Year editing functions
        function showEditYear() {
            if (currentUser && currentUser.role === 'superadmin') {
                document.getElementById('editYearModal').classList.remove('hidden');
                document.getElementById('editActiveYear').value = systemData.activeYear;
            } else {
                showNotification('Hanya super admin yang dapat mengedit tahun aktif', 'error');
            }
        }

        function hideEditYear() {
            document.getElementById('editYearModal').classList.add('hidden');
        }

        function handleEditYear(event) {
            event.preventDefault();
            
            if (!currentUser || currentUser.role !== 'superadmin') {
                showNotification('Hanya super admin yang dapat mengedit tahun aktif', 'error');
                return;
            }

            const newYear = parseInt(document.getElementById('editActiveYear').value);
            
            if (newYear < 2020 || newYear > 2030) {
                showNotification('Tahun harus antara 2020-2030', 'error');
                return;
            }

            systemData.activeYear = newYear;
            updateStats();
            hideEditYear();
            showNotification('Tahun aktif berhasil diperbarui!', 'success');
        }

        // Profile menu toggle function
        function toggleProfileMenu() {
            const dropdown = document.getElementById('profileDropdown');
            dropdown.classList.toggle('hidden');
        }

        // Close dropdown when clicking outside
        document.addEventListener('click', function(event) {
            const profileMenu = document.getElementById('userProfileMenu');
            const dropdown = document.getElementById('profileDropdown');
            
            if (profileMenu && !profileMenu.contains(event.target)) {
                dropdown.classList.add('hidden');
            }
        });

        // User management functions
        function showAddUser() {
            if (currentUser && currentUser.role === 'superadmin') {
                document.getElementById('addUserModal').classList.remove('hidden');
            } else {
                showNotification('Hanya super admin yang dapat menambah pengguna', 'error');
            }
        }

        function hideAddUser() {
            document.getElementById('addUserModal').classList.add('hidden');
            document.getElementById('newUserName').value = '';
            document.getElementById('newUserUsername').value = '';
            document.getElementById('newUserEmail').value = '';
            document.getElementById('newUserPassword').value = '';
            document.getElementById('newUserRole').value = '';
        }

        function handleAddUser(event) {
            event.preventDefault();
            
            if (!currentUser || currentUser.role !== 'superadmin') {
                showNotification('Hanya super admin yang dapat menambah pengguna', 'error');
                return;
            }

            const name = document.getElementById('newUserName').value;
            const username = document.getElementById('newUserUsername').value;
            const email = document.getElementById('newUserEmail').value;
            const password = document.getElementById('newUserPassword').value;
            const role = document.getElementById('newUserRole').value;

            // Check if username already exists
            if (usersData.find(u => u.username === username)) {
                showNotification('Username sudah digunakan!', 'error');
                return;
            }

            // Check if email already exists
            if (usersData.find(u => u.email === email)) {
                showNotification('Email sudah digunakan!', 'error');
                return;
            }

            const newUser = {
                id: Math.max(...usersData.map(u => u.id)) + 1,
                username: username,
                password: password,
                name: name,
                role: role,
                email: email,
                createdDate: new Date().toISOString().split('T')[0]
            };

            usersData.push(newUser);
            renderUsers();
            hideAddUser();
            showNotification('Pengguna berhasil ditambahkan!', 'success');
        }

        function showEditUser(userId) {
            if (!currentUser || currentUser.role !== 'superadmin') {
                showNotification('Hanya super admin yang dapat mengedit pengguna', 'error');
                return;
            }

            const user = usersData.find(u => u.id === userId);
            if (user) {
                document.getElementById('editUserId').value = user.id;
                document.getElementById('editUserName').value = user.name;
                document.getElementById('editUserUsername').value = user.username;
                document.getElementById('editUserEmail').value = user.email;
                document.getElementById('editUserPassword').value = '';
                document.getElementById('editUserRole').value = user.role;
                document.getElementById('editUserModal').classList.remove('hidden');
            }
        }

        function hideEditUser() {
            document.getElementById('editUserModal').classList.add('hidden');
        }

        function handleEditUser(event) {
            event.preventDefault();
            
            if (!currentUser || currentUser.role !== 'superadmin') {
                showNotification('Hanya super admin yang dapat mengedit pengguna', 'error');
                return;
            }

            const userId = parseInt(document.getElementById('editUserId').value);
            const name = document.getElementById('editUserName').value;
            const username = document.getElementById('editUserUsername').value;
            const email = document.getElementById('editUserEmail').value;
            const password = document.getElementById('editUserPassword').value;
            const role = document.getElementById('editUserRole').value;

            const userIndex = usersData.findIndex(u => u.id === userId);
            if (userIndex !== -1) {
                // Check if username is taken by another user
                const existingUser = usersData.find(u => u.username === username && u.id !== userId);
                if (existingUser) {
                    showNotification('Username sudah digunakan oleh pengguna lain!', 'error');
                    return;
                }

                // Check if email is taken by another user
                const existingEmail = usersData.find(u => u.email === email && u.id !== userId);
                if (existingEmail) {
                    showNotification('Email sudah digunakan oleh pengguna lain!', 'error');
                    return;
                }

                usersData[userIndex].name = name;
                usersData[userIndex].username = username;
                usersData[userIndex].email = email;
                usersData[userIndex].role = role;
                
                // Only update password if provided
                if (password.trim() !== '') {
                    usersData[userIndex].password = password;
                }

                renderUsers();
                hideEditUser();
                showNotification('Pengguna berhasil diperbarui!', 'success');
            }
        }

        function deleteUser(userId) {
            if (!currentUser || currentUser.role !== 'superadmin') {
                showNotification('Hanya super admin yang dapat menghapus pengguna', 'error');
                return;
            }

            // Prevent deleting superadmin
            const user = usersData.find(u => u.id === userId);
            if (user && user.role === 'superadmin') {
                showNotification('Super admin tidak dapat dihapus!', 'error');
                return;
            }

            // Prevent deleting current user
            if (currentUser.id === userId) {
                showNotification('Anda tidak dapat menghapus akun sendiri!', 'error');
                return;
            }

            if (confirm('Apakah Anda yakin ingin menghapus pengguna ini?')) {
                usersData = usersData.filter(u => u.id !== userId);
                renderUsers();
                showNotification('Pengguna berhasil dihapus!', 'success');
            }
        }

        function renderUsers() {
            const tbody = document.getElementById('usersTableBody');
            tbody.innerHTML = '';

            usersData.forEach(user => {
                const row = document.createElement('tr');
                row.className = 'hover:bg-gray-50';
                
                const roleColors = {
                    'superadmin': 'bg-red-100 text-red-800',
                    'admin': 'bg-blue-100 text-blue-800',
                    'user': 'bg-green-100 text-green-800'
                };

                const roleLabels = {
                    'superadmin': 'Super Admin',
                    'admin': 'Admin',
                    'user': 'User'
                };

                row.innerHTML = `
                    <td class="px-6 py-4 whitespace-nowrap">
                        <div class="flex items-center">
                            <div class="w-10 h-10 bg-gray-300 rounded-full flex items-center justify-center">
                                <i class="fas fa-user text-gray-600"></i>
                            </div>
                            <div class="ml-4">
                                <div class="text-sm font-medium text-gray-900">${user.name}</div>
                                <div class="text-sm text-gray-500">@${user.username}</div>
                            </div>
                        </div>
                    </td>
                    <td class="px-6 py-4 whitespace-nowrap">
                        <span class="px-2 inline-flex text-xs leading-5 font-semibold rounded-full ${roleColors[user.role]}">
                            ${roleLabels[user.role]}
                        </span>
                    </td>
                    <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-900">
                        ${user.email}
                    </td>
                    <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">
                        ${formatDate(user.createdDate)}
                    </td>
                    <td class="px-6 py-4 whitespace-nowrap text-sm font-medium">
                        <div class="flex space-x-2">
                            <button onclick="showEditUser(${user.id})" class="text-blue-600 hover:text-blue-900 transition-colors">
                                <i class="fas fa-edit"></i>
                            </button>
                            ${user.role !== 'superadmin' && user.id !== currentUser.id ? 
                                `<button onclick="deleteUser(${user.id})" class="text-red-600 hover:text-red-900 transition-colors">
                                    <i class="fas fa-trash"></i>
                                </button>` : ''
                            }
                        </div>
                    </td>
                `;
                
                tbody.appendChild(row);
            });
        }

        // Gallery functions
        function showAddGallery() {
            if (currentUser && (currentUser.role === 'admin' || currentUser.role === 'superadmin')) {
                document.getElementById('addGalleryModal').classList.remove('hidden');
            } else {
                showNotification('Hanya admin dan super admin yang dapat menambah foto galeri', 'error');
            }
        }

        function hideAddGallery() {
            document.getElementById('addGalleryModal').classList.add('hidden');
            document.getElementById('galleryTitle').value = '';
            document.getElementById('galleryCategory').value = '';
            document.getElementById('galleryDate').value = '';
            document.getElementById('galleryDescription').value = '';
            document.getElementById('galleryImage').value = '';
            document.getElementById('galleryImagePreview').classList.add('hidden');
            selectedGalleryImage = null;
        }

        function handleGalleryImageUpload(event) {
            const file = event.target.files[0];
            if (file) {
                // Check file size (max 5MB)
                if (file.size > 5 * 1024 * 1024) {
                    showNotification('Ukuran file terlalu besar. Maksimal 5MB.', 'error');
                    event.target.value = '';
                    return;
                }

                // Check file type
                if (!file.type.startsWith('image/')) {
                    showNotification('File harus berupa gambar.', 'error');
                    event.target.value = '';
                    return;
                }

                const reader = new FileReader();
                reader.onload = function(e) {
                    selectedGalleryImage = e.target.result;
                    document.getElementById('galleryImagePreviewImg').src = selectedGalleryImage;
                    document.getElementById('galleryImagePreview').classList.remove('hidden');
                };
                reader.readAsDataURL(file);
            }
        }

        function removeGalleryImage() {
            selectedGalleryImage = null;
            document.getElementById('galleryImage').value = '';
            document.getElementById('galleryImagePreview').classList.add('hidden');
        }

        function handleAddGallery(event) {
            event.preventDefault();
            
            if (!currentUser || (currentUser.role !== 'admin' && currentUser.role !== 'superadmin')) {
                showNotification('Hanya admin dan super admin yang dapat menambah foto galeri', 'error');
                return;
            }

            const title = document.getElementById('galleryTitle').value;
            const category = document.getElementById('galleryCategory').value;
            const galleryDate = document.getElementById('galleryDate').value;
            const description = document.getElementById('galleryDescription').value;

            const newGallery = {
                id: galleryData.length + 1,
                title: title,
                category: category,
                description: description,
                date: galleryDate,
                image: selectedGalleryImage
            };

            galleryData.unshift(newGallery);
            renderGallery();
            initializeSlider();
            hideAddGallery();
            showNotification('Foto berhasil ditambahkan ke galeri!', 'success');
        }

        function renderGallery() {
            const galleryGrid = document.getElementById('galleryGrid');
            galleryGrid.innerHTML = '';

            galleryData.forEach(item => {
                const galleryCard = document.createElement('div');
                galleryCard.className = 'gallery-item bg-white rounded-lg shadow-md overflow-hidden cursor-pointer';
                galleryCard.onclick = () => showGalleryView(item.id);
                
                galleryCard.innerHTML = `
                    <div class="h-48 overflow-hidden">
                        <img src="${item.image}" alt="${item.title}" class="w-full h-full object-cover">
                    </div>
                    <div class="p-4">
                        <div class="flex justify-between items-start mb-2">
                            <span class="bg-purple-100 text-purple-800 text-xs font-semibold px-2.5 py-0.5 rounded">${item.category}</span>
                            ${currentUser && (currentUser.role === 'admin' || currentUser.role === 'superadmin') ? 
                                `<button onclick="event.stopPropagation(); deleteGallery(${item.id})" class="text-red-500 hover:text-red-700 transition-colors">
                                    <i class="fas fa-trash text-sm"></i>
                                </button>` : ''
                            }
                        </div>
                        <h3 class="font-semibold text-gray-800 text-sm mb-2">${item.title}</h3>
                        <p class="text-gray-600 text-xs mb-2 line-clamp-2">${item.description.substring(0, 80)}...</p>
                        <p class="text-xs text-gray-500">
                            <i class="fas fa-calendar mr-1"></i>${formatDate(item.date)}
                        </p>
                    </div>
                `;
                
                galleryGrid.appendChild(galleryCard);
            });
        }

        function showGalleryView(id) {
            const item = galleryData.find(g => g.id === id);
            if (item) {
                currentViewingGallery = item;
                
                document.getElementById('galleryViewImage').innerHTML = `
                    <img src="${item.image}" alt="${item.title}" class="w-full h-full object-cover">
                `;
                document.getElementById('galleryViewTitle').textContent = item.title;
                document.getElementById('galleryViewCategory').textContent = item.category;
                document.getElementById('galleryViewDescription').textContent = item.description;
                document.getElementById('galleryViewDate').innerHTML = `<i class="fas fa-calendar mr-1"></i>Tanggal: ${formatDate(item.date)}`;
                
                // Show delete button for admin/superadmin
                const deleteBtn = document.getElementById('deleteGalleryBtn');
                if (currentUser && (currentUser.role === 'admin' || currentUser.role === 'superadmin')) {
                    deleteBtn.classList.remove('hidden');
                } else {
                    deleteBtn.classList.add('hidden');
                }
                
                document.getElementById('galleryViewModal').classList.remove('hidden');
            }
        }

        function hideGalleryView() {
            document.getElementById('galleryViewModal').classList.add('hidden');
            currentViewingGallery = null;
        }

        function deleteGallery(id) {
            if (!currentUser || (currentUser.role !== 'admin' && currentUser.role !== 'superadmin')) {
                showNotification('Hanya admin dan super admin yang dapat menghapus foto galeri', 'error');
                return;
            }

            if (confirm('Apakah Anda yakin ingin menghapus foto ini dari galeri?')) {
                galleryData = galleryData.filter(item => item.id !== id);
                renderGallery();
                initializeSlider();
                showNotification('Foto berhasil dihapus dari galeri!', 'success');
            }
        }

        function deleteGalleryItem() {
            if (currentViewingGallery) {
                deleteGallery(currentViewingGallery.id);
                hideGalleryView();
            }
        }

        // Slider functions
        function initializeSlider() {
            const slider = document.getElementById('gallerySlider');
            const indicators = document.getElementById('slideIndicators');
            
            if (galleryData.length === 0) {
                slider.innerHTML = '<div class="flex items-center justify-center h-full bg-gray-200 text-gray-500">Belum ada foto dalam galeri</div>';
                indicators.innerHTML = '';
                return;
            }

            // Clear existing content
            slider.innerHTML = '';
            indicators.innerHTML = '';

            // Create slides
            galleryData.forEach((item, index) => {
                const slide = document.createElement('div');
                slide.className = `absolute inset-0 gallery-slide ${index === 0 ? 'opacity-100' : 'opacity-0'}`;
                slide.style.transform = `translateX(${index * 100}%)`;
                
                slide.innerHTML = `
                    <div class="relative h-full cursor-pointer" onclick="showGalleryView(${item.id})">
                        <img src="${item.image}" alt="${item.title}" class="w-full h-full object-cover">
                        <div class="absolute bottom-0 left-0 right-0 bg-gradient-to-t from-black to-transparent p-6">
                            <span class="bg-purple-600 text-white text-xs font-semibold px-3 py-1 rounded mb-2 inline-block">${item.category}</span>
                            <h3 class="text-white text-xl font-bold mb-2">${item.title}</h3>
                            <p class="text-gray-200 text-sm">${item.description.substring(0, 100)}...</p>
                        </div>
                    </div>
                `;
                
                slider.appendChild(slide);

                // Create indicator
                const indicator = document.createElement('button');
                indicator.className = `w-3 h-3 rounded-full transition-all ${index === 0 ? 'bg-white' : 'bg-white bg-opacity-50'}`;
                indicator.onclick = () => goToSlide(index);
                indicators.appendChild(indicator);
            });

            // Start auto-slide
            startAutoSlide();
        }

        function changeSlide(direction) {
            if (galleryData.length === 0) return;
            
            const newSlide = currentSlide + direction;
            
            if (newSlide >= galleryData.length) {
                goToSlide(0);
            } else if (newSlide < 0) {
                goToSlide(galleryData.length - 1);
            } else {
                goToSlide(newSlide);
            }
        }

        function goToSlide(slideIndex) {
            if (galleryData.length === 0) return;
            
            const slides = document.querySelectorAll('#gallerySlider .gallery-slide');
            const indicators = document.querySelectorAll('#slideIndicators button');
            
            // Hide current slide
            if (slides[currentSlide]) {
                slides[currentSlide].classList.remove('opacity-100');
                slides[currentSlide].classList.add('opacity-0');
            }
            if (indicators[currentSlide]) {
                indicators[currentSlide].classList.remove('bg-white');
                indicators[currentSlide].classList.add('bg-white', 'bg-opacity-50');
            }
            
            // Show new slide
            currentSlide = slideIndex;
            if (slides[currentSlide]) {
                slides[currentSlide].classList.remove('opacity-0');
                slides[currentSlide].classList.add('opacity-100');
            }
            if (indicators[currentSlide]) {
                indicators[currentSlide].classList.remove('bg-opacity-50');
                indicators[currentSlide].classList.add('bg-white');
            }
            
            // Reset auto-slide timer
            startAutoSlide();
        }

        function startAutoSlide() {
            // Clear existing interval
            if (slideInterval) {
                clearInterval(slideInterval);
            }
            
            // Start new interval (change slide every 5 seconds)
            slideInterval = setInterval(() => {
                if (galleryData.length > 1) {
                    changeSlide(1);
                }
            }, 5000);
        }

        function stopAutoSlide() {
            if (slideInterval) {
                clearInterval(slideInterval);
                slideInterval = null;
            }
        }

        // Pause auto-slide when hovering over slider
        document.addEventListener('DOMContentLoaded', function() {
            const slider = document.getElementById('gallerySlider');
            if (slider) {
                slider.addEventListener('mouseenter', stopAutoSlide);
                slider.addEventListener('mouseleave', startAutoSlide);
            }
        });

        // Gallery functions
        function showAddGallery() {
            if (currentUser && (currentUser.role === 'admin' || currentUser.role === 'superadmin')) {
                document.getElementById('addGalleryModal').classList.remove('hidden');
            } else {
                showNotification('Hanya admin dan super admin yang dapat menambah foto galeri', 'error');
            }
        }

        function hideAddGallery() {
            document.getElementById('addGalleryModal').classList.add('hidden');
            document.getElementById('galleryTitle').value = '';
            document.getElementById('galleryCategory').value = '';
            document.getElementById('galleryDate').value = '';
            document.getElementById('galleryDescription').value = '';
            document.getElementById('galleryImage').value = '';
            document.getElementById('galleryImagePreview').classList.add('hidden');
            selectedGalleryImage = null;
        }

        function handleGalleryImageUpload(event) {
            const file = event.target.files[0];
            if (file) {
                // Check file size (max 5MB)
                if (file.size > 5 * 1024 * 1024) {
                    showNotification('Ukuran file terlalu besar. Maksimal 5MB.', 'error');
                    event.target.value = '';
                    return;
                }

                // Check file type
                if (!file.type.startsWith('image/')) {
                    showNotification('File harus berupa gambar.', 'error');
                    event.target.value = '';
                    return;
                }

                const reader = new FileReader();
                reader.onload = function(e) {
                    selectedGalleryImage = e.target.result;
                    document.getElementById('galleryImagePreviewImg').src = selectedGalleryImage;
                    document.getElementById('galleryImagePreview').classList.remove('hidden');
                };
                reader.readAsDataURL(file);
            }
        }

        function removeGalleryImage() {
            selectedGalleryImage = null;
            document.getElementById('galleryImage').value = '';
            document.getElementById('galleryImagePreview').classList.add('hidden');
        }

        function handleAddGallery(event) {
            event.preventDefault();
            
            if (!currentUser || (currentUser.role !== 'admin' && currentUser.role !== 'superadmin')) {
                showNotification('Hanya admin dan super admin yang dapat menambah foto galeri', 'error');
                return;
            }

            const title = document.getElementById('galleryTitle').value;
            const category = document.getElementById('galleryCategory').value;
            const galleryDate = document.getElementById('galleryDate').value;
            const description = document.getElementById('galleryDescription').value;

            const newGallery = {
                id: galleryData.length + 1,
                title: title,
                category: category,
                description: description,
                date: galleryDate,
                image: selectedGalleryImage
            };

            galleryData.unshift(newGallery);
            renderGallery();
            initializeSlider();
            initializeHomepageSlider();
            hideAddGallery();
            showNotification('Foto berhasil ditambahkan ke galeri!', 'success');
        }

        function renderGallery() {
            const galleryGrid = document.getElementById('galleryGrid');
            if (!galleryGrid) return;
            
            galleryGrid.innerHTML = '';

            galleryData.forEach(item => {
                const galleryCard = document.createElement('div');
                galleryCard.className = 'gallery-item bg-white rounded-lg shadow-md overflow-hidden cursor-pointer hover:shadow-lg transition-shadow';
                galleryCard.onclick = () => showGalleryView(item.id);
                
                galleryCard.innerHTML = `
                    <div class="h-48 overflow-hidden">
                        <img src="${item.image}" alt="${item.title}" class="w-full h-full object-cover hover:scale-105 transition-transform duration-300">
                    </div>
                    <div class="p-4">
                        <div class="flex justify-between items-start mb-2">
                            <span class="bg-purple-100 text-purple-800 text-xs font-semibold px-2.5 py-0.5 rounded">${item.category}</span>
                            ${currentUser && (currentUser.role === 'admin' || currentUser.role === 'superadmin') ? 
                                `<button onclick="event.stopPropagation(); deleteGallery(${item.id})" class="text-red-500 hover:text-red-700 transition-colors">
                                    <i class="fas fa-trash text-sm"></i>
                                </button>` : ''
                            }
                        </div>
                        <h3 class="font-semibold text-gray-800 text-sm mb-2">${item.title}</h3>
                        <p class="text-gray-600 text-xs mb-2 line-clamp-2">${item.description.substring(0, 80)}...</p>
                        <p class="text-xs text-gray-500">
                            <i class="fas fa-calendar mr-1"></i>${formatDate(item.date)}
                        </p>
                    </div>
                `;
                
                galleryGrid.appendChild(galleryCard);
            });
        }

        function showGalleryView(id) {
            const item = galleryData.find(g => g.id === id);
            if (item) {
                currentViewingGallery = item;
                
                document.getElementById('galleryViewImage').innerHTML = `
                    <img src="${item.image}" alt="${item.title}" class="w-full h-full object-cover">
                `;
                document.getElementById('galleryViewTitle').textContent = item.title;
                document.getElementById('galleryViewCategory').textContent = item.category;
                document.getElementById('galleryViewDescription').textContent = item.description;
                document.getElementById('galleryViewDate').innerHTML = `<i class="fas fa-calendar mr-1"></i>Tanggal: ${formatDate(item.date)}`;
                
                // Show delete button for admin/superadmin
                const deleteBtn = document.getElementById('deleteGalleryBtn');
                if (currentUser && (currentUser.role === 'admin' || currentUser.role === 'superadmin')) {
                    deleteBtn.classList.remove('hidden');
                } else {
                    deleteBtn.classList.add('hidden');
                }
                
                document.getElementById('galleryViewModal').classList.remove('hidden');
            }
        }

        function hideGalleryView() {
            document.getElementById('galleryViewModal').classList.add('hidden');
            currentViewingGallery = null;
        }

        function deleteGallery(id) {
            if (!currentUser || (currentUser.role !== 'admin' && currentUser.role !== 'superadmin')) {
                showNotification('Hanya admin dan super admin yang dapat menghapus foto galeri', 'error');
                return;
            }

            if (confirm('Apakah Anda yakin ingin menghapus foto ini dari galeri?')) {
                galleryData = galleryData.filter(item => item.id !== id);
                renderGallery();
                initializeSlider();
                initializeHomepageSlider();
                showNotification('Foto berhasil dihapus dari galeri!', 'success');
            }
        }

        function deleteGalleryItem() {
            if (currentViewingGallery) {
                deleteGallery(currentViewingGallery.id);
                hideGalleryView();
            }
        }

        // Slider functions
        function initializeSlider() {
            const slider = document.getElementById('gallerySlider');
            const indicators = document.getElementById('slideIndicators');
            
            if (!slider || !indicators) return;
            
            if (galleryData.length === 0) {
                slider.innerHTML = '<div class="flex items-center justify-center h-full bg-gray-200 text-gray-500">Belum ada foto dalam galeri</div>';
                indicators.innerHTML = '';
                return;
            }

            // Clear existing content
            slider.innerHTML = '';
            indicators.innerHTML = '';

            // Create slides
            galleryData.forEach((item, index) => {
                const slide = document.createElement('div');
                slide.className = `absolute inset-0 gallery-slide transition-opacity duration-500 ${index === 0 ? 'opacity-100' : 'opacity-0'}`;
                
                slide.innerHTML = `
                    <div class="relative h-full cursor-pointer" onclick="showGalleryView(${item.id})">
                        <img src="${item.image}" alt="${item.title}" class="w-full h-full object-cover">
                        <div class="absolute bottom-0 left-0 right-0 bg-gradient-to-t from-black to-transparent p-6">
                            <span class="bg-purple-600 text-white text-xs font-semibold px-3 py-1 rounded mb-2 inline-block">${item.category}</span>
                            <h3 class="text-white text-xl font-bold mb-2">${item.title}</h3>
                            <p class="text-gray-200 text-sm">${item.description.substring(0, 100)}...</p>
                        </div>
                    </div>
                `;
                
                slider.appendChild(slide);

                // Create indicator
                const indicator = document.createElement('button');
                indicator.className = `w-3 h-3 rounded-full transition-all ${index === 0 ? 'bg-white' : 'bg-white bg-opacity-50'}`;
                indicator.onclick = () => goToSlide(index);
                indicators.appendChild(indicator);
            });

            // Start auto-slide
            startAutoSlide();
        }

        function initializeHomepageSlider() {
            const slider = document.getElementById('homepageSlider');
            const indicators = document.getElementById('homepageSlideIndicators');
            
            if (!slider || !indicators) return;
            
            // Combine gallery and announcement data for homepage slider
            const homepageItems = [];
            
            // Add gallery items with images
            galleryData.slice(0, 3).forEach(item => {
                homepageItems.push({
                    type: 'gallery',
                    id: item.id,
                    title: item.title,
                    category: item.category,
                    description: item.description,
                    date: item.date,
                    image: item.image,
                    action: () => showSection('galeri')
                });
            });
            
            // Add announcements with images
            announcementData.filter(item => item.image).slice(0, 3).forEach(item => {
                homepageItems.push({
                    type: 'announcement',
                    id: item.id,
                    title: item.title,
                    category: item.category,
                    description: item.content,
                    date: item.date,
                    image: item.image,
                    priority: item.priority,
                    action: () => showSection('pengumuman')
                });
            });
            
            // Add news with images
            newsData.filter(item => item.image).slice(0, 2).forEach(item => {
                homepageItems.push({
                    type: 'news',
                    id: item.id,
                    title: item.title,
                    category: item.category,
                    description: item.content,
                    date: item.date,
                    image: item.image,
                    author: item.author,
                    action: () => showSection('berita')
                });
            });
            
            // Sort by date (newest first)
            homepageItems.sort((a, b) => new Date(b.date) - new Date(a.date));
            
            // Take only first 8 items
            const finalItems = homepageItems.slice(0, 8);
            
            if (finalItems.length === 0) {
                slider.innerHTML = '<div class="flex items-center justify-center h-full bg-gray-200 text-gray-500">Belum ada konten dengan gambar</div>';
                indicators.innerHTML = '';
                return;
            }

            // Clear existing content
            slider.innerHTML = '';
            indicators.innerHTML = '';

            // Create slides
            finalItems.forEach((item, index) => {
                const slide = document.createElement('div');
                slide.className = `absolute inset-0 homepage-slide transition-opacity duration-500 ${index === 0 ? 'opacity-100' : 'opacity-0'}`;
                
                // Determine badge color and icon based on type
                let badgeClass = '';
                let badgeIcon = '';
                let badgeText = '';
                
                switch(item.type) {
                    case 'gallery':
                        badgeClass = 'bg-purple-600';
                        badgeIcon = 'fas fa-images';
                        badgeText = 'Galeri';
                        break;
                    case 'announcement':
                        badgeClass = item.priority === 'Tinggi' ? 'bg-red-600' : item.priority === 'Sedang' ? 'bg-yellow-600' : 'bg-green-600';
                        badgeIcon = 'fas fa-bullhorn';
                        badgeText = 'Pengumuman';
                        break;
                    case 'news':
                        badgeClass = 'bg-blue-600';
                        badgeIcon = 'fas fa-newspaper';
                        badgeText = 'Berita';
                        break;
                }
                
                const clickAction = item.type === 'gallery' ? 'showSection(\'galeri\')' : 
                                  item.type === 'announcement' ? 'showSection(\'pengumuman\')' : 
                                  'showSection(\'berita\')';
                
                slide.innerHTML = `
                    <div class="relative h-full cursor-pointer" onclick="${clickAction}">
                        <img src="${item.image}" alt="${item.title}" class="w-full h-full object-cover">
                        <div class="absolute inset-0 bg-black bg-opacity-30"></div>
                        <div class="absolute top-4 left-4">
                            <span class="${badgeClass} text-white text-xs font-semibold px-3 py-1 rounded-full">
                                <i class="${badgeIcon} mr-1"></i>${badgeText}
                            </span>
                        </div>
                        <div class="absolute bottom-0 left-0 right-0 bg-gradient-to-t from-black to-transparent p-6">
                            <div class="mb-2">
                                <span class="bg-white bg-opacity-20 text-white text-xs font-semibold px-2 py-1 rounded backdrop-blur-sm">
                                    ${item.category}
                                </span>
                                ${item.priority ? `<span class="ml-2 bg-white bg-opacity-20 text-white text-xs font-semibold px-2 py-1 rounded backdrop-blur-sm">
                                    ${item.priority} Prioritas
                                </span>` : ''}
                            </div>
                            <h3 class="text-white text-xl font-bold mb-2 leading-tight">${item.title}</h3>
                            <p class="text-gray-200 text-sm mb-2 leading-relaxed">${item.description.substring(0, 120)}...</p>
                            <div class="flex justify-between items-center text-xs text-gray-300">
                                <span><i class="fas fa-calendar mr-1"></i>${formatDate(item.date)}</span>
                                ${item.author ? `<span><i class="fas fa-user mr-1"></i>${item.author}</span>` : ''}
                            </div>
                        </div>
                    </div>
                `;
                
                slider.appendChild(slide);

                // Create indicator
                const indicator = document.createElement('button');
                indicator.className = `w-2 h-2 rounded-full transition-all ${index === 0 ? 'bg-white' : 'bg-white bg-opacity-50'}`;
                indicator.onclick = () => goToHomepageSlide(index);
                indicators.appendChild(indicator);
            });

            // Store items for navigation
            window.homepageSliderItems = finalItems;

            // Start auto-slide
            startHomepageAutoSlide();
        }

        function changeSlide(direction) {
            if (galleryData.length === 0) return;
            
            const newSlide = currentSlide + direction;
            
            if (newSlide >= galleryData.length) {
                goToSlide(0);
            } else if (newSlide < 0) {
                goToSlide(galleryData.length - 1);
            } else {
                goToSlide(newSlide);
            }
        }

        function changeHomepageSlide(direction) {
            const homepageItems = window.homepageSliderItems || [];
            if (homepageItems.length === 0) return;
            
            const newSlide = currentHomepageSlide + direction;
            
            if (newSlide >= homepageItems.length) {
                goToHomepageSlide(0);
            } else if (newSlide < 0) {
                goToHomepageSlide(homepageItems.length - 1);
            } else {
                goToHomepageSlide(newSlide);
            }
        }

        function goToSlide(slideIndex) {
            if (galleryData.length === 0) return;
            
            const slides = document.querySelectorAll('#gallerySlider .gallery-slide');
            const indicators = document.querySelectorAll('#slideIndicators button');
            
            // Hide current slide
            if (slides[currentSlide]) {
                slides[currentSlide].classList.remove('opacity-100');
                slides[currentSlide].classList.add('opacity-0');
            }
            if (indicators[currentSlide]) {
                indicators[currentSlide].classList.remove('bg-white');
                indicators[currentSlide].classList.add('bg-white', 'bg-opacity-50');
            }
            
            // Show new slide
            currentSlide = slideIndex;
            if (slides[currentSlide]) {
                slides[currentSlide].classList.remove('opacity-0');
                slides[currentSlide].classList.add('opacity-100');
            }
            if (indicators[currentSlide]) {
                indicators[currentSlide].classList.remove('bg-opacity-50');
                indicators[currentSlide].classList.add('bg-white');
            }
            
            // Reset auto-slide timer
            startAutoSlide();
        }

        function goToHomepageSlide(slideIndex) {
            const homepageItems = window.homepageSliderItems || [];
            if (homepageItems.length === 0) return;
            
            const slides = document.querySelectorAll('#homepageSlider .homepage-slide');
            const indicators = document.querySelectorAll('#homepageSlideIndicators button');
            
            // Hide current slide
            if (slides[currentHomepageSlide]) {
                slides[currentHomepageSlide].classList.remove('opacity-100');
                slides[currentHomepageSlide].classList.add('opacity-0');
            }
            if (indicators[currentHomepageSlide]) {
                indicators[currentHomepageSlide].classList.remove('bg-white');
                indicators[currentHomepageSlide].classList.add('bg-white', 'bg-opacity-50');
            }
            
            // Show new slide
            currentHomepageSlide = slideIndex;
            if (slides[currentHomepageSlide]) {
                slides[currentHomepageSlide].classList.remove('opacity-0');
                slides[currentHomepageSlide].classList.add('opacity-100');
            }
            if (indicators[currentHomepageSlide]) {
                indicators[currentHomepageSlide].classList.remove('bg-opacity-50');
                indicators[currentHomepageSlide].classList.add('bg-white');
            }
            
            // Reset auto-slide timer
            startHomepageAutoSlide();
        }

        function startAutoSlide() {
            // Clear existing interval
            if (slideInterval) {
                clearInterval(slideInterval);
            }
            
            // Start new interval (change slide every 5 seconds)
            slideInterval = setInterval(() => {
                if (galleryData.length > 1) {
                    changeSlide(1);
                }
            }, 5000);
        }

        function startHomepageAutoSlide() {
            // Clear existing interval
            if (homepageSlideInterval) {
                clearInterval(homepageSlideInterval);
            }
            
            // Start new interval (change slide every 4 seconds)
            homepageSlideInterval = setInterval(() => {
                const homepageItems = window.homepageSliderItems || [];
                if (homepageItems.length > 1) {
                    changeHomepageSlide(1);
                }
            }, 4000);
        }

        function stopAutoSlide() {
            if (slideInterval) {
                clearInterval(slideInterval);
                slideInterval = null;
            }
        }

        function stopHomepageAutoSlide() {
            if (homepageSlideInterval) {
                clearInterval(homepageSlideInterval);
                homepageSlideInterval = null;
            }
        }

        // Service functions
        function showAddService() {
            if (currentUser && (currentUser.role === 'admin' || currentUser.role === 'superadmin')) {
                document.getElementById('addServiceModal').classList.remove('hidden');
            } else {
                showNotification('Hanya admin dan super admin yang dapat menambah layanan', 'error');
            }
        }

        function hideAddService() {
            document.getElementById('addServiceModal').classList.add('hidden');
            document.getElementById('serviceName').value = '';
            document.getElementById('serviceCategory').value = '';
            document.getElementById('serviceType').value = '';
            document.getElementById('serviceTime').value = '';
            document.getElementById('serviceCost').value = '';
            document.getElementById('serviceRequirements').value = '';
            document.getElementById('serviceProcedure').value = '';
            document.getElementById('serviceDescription').value = '';
        }

        function handleAddService(event) {
            event.preventDefault();
            
            if (!currentUser || (currentUser.role !== 'admin' && currentUser.role !== 'superadmin')) {
                showNotification('Hanya admin dan super admin yang dapat menambah layanan', 'error');
                return;
            }

            const name = document.getElementById('serviceName').value;
            const category = document.getElementById('serviceCategory').value;
            const type = document.getElementById('serviceType').value;
            const time = document.getElementById('serviceTime').value;
            const cost = document.getElementById('serviceCost').value;
            const requirementsText = document.getElementById('serviceRequirements').value;
            const procedureText = document.getElementById('serviceProcedure').value;
            const description = document.getElementById('serviceDescription').value;

            const requirements = requirementsText.split('\n').filter(line => line.trim() !== '');
            const procedure = procedureText.split('\n').filter(line => line.trim() !== '');

            const newService = {
                id: servicesData.length + 1,
                name: name,
                category: category,
                type: type,
                time: time,
                cost: cost,
                description: description,
                requirements: requirements,
                procedure: procedure
            };

            servicesData.push(newService);
            renderServices();
            hideAddService();
            showNotification('Layanan berhasil ditambahkan!', 'success');
        }

        function filterServices(category) {
            currentServiceFilter = category;
            
            // Update filter button styles
            document.querySelectorAll('.service-filter-btn').forEach(btn => {
                btn.classList.remove('bg-indigo-600', 'text-white');
                btn.classList.add('bg-gray-200', 'text-gray-700', 'hover:bg-gray-300');
            });
            
            event.target.classList.remove('bg-gray-200', 'text-gray-700', 'hover:bg-gray-300');
            event.target.classList.add('bg-indigo-600', 'text-white');
            
            renderServices();
        }

        function renderServices() {
            const servicesGrid = document.getElementById('servicesGrid');
            servicesGrid.innerHTML = '';

            const filteredServices = currentServiceFilter === 'all' 
                ? servicesData 
                : servicesData.filter(service => service.category === currentServiceFilter);

            if (filteredServices.length === 0) {
                servicesGrid.innerHTML = '<div class="col-span-full text-center py-8 text-gray-500">Tidak ada layanan dalam kategori ini</div>';
                return;
            }

            filteredServices.forEach(service => {
                const serviceCard = document.createElement('div');
                serviceCard.className = 'bg-white rounded-lg shadow-md p-6 hover:shadow-lg transition-shadow cursor-pointer';
                serviceCard.onclick = () => showServiceDetail(service.id);
                
                const categoryColors = {
                    'kepegawaian': 'bg-blue-100 text-blue-800',
                    'diklat': 'bg-green-100 text-green-800',
                    'informasi': 'bg-yellow-100 text-yellow-800',
                    'konsultasi': 'bg-purple-100 text-purple-800'
                };

                const typeColors = {
                    'online': 'bg-green-100 text-green-800',
                    'offline': 'bg-red-100 text-red-800',
                    'hybrid': 'bg-blue-100 text-blue-800'
                };

                const categoryLabels = {
                    'kepegawaian': 'Kepegawaian',
                    'diklat': 'Diklat & Pengembangan',
                    'informasi': 'Informasi',
                    'konsultasi': 'Konsultasi'
                };

                const typeLabels = {
                    'online': 'Online',
                    'offline': 'Offline',
                    'hybrid': 'Online & Offline'
                };
                
                serviceCard.innerHTML = `
                    <div class="flex justify-between items-start mb-4">
                        <div class="flex flex-wrap gap-2">
                            <span class="text-xs font-semibold px-2.5 py-0.5 rounded ${categoryColors[service.category]}">
                                ${categoryLabels[service.category]}
                            </span>
                            <span class="text-xs font-semibold px-2.5 py-0.5 rounded ${typeColors[service.type]}">
                                ${typeLabels[service.type]}
                            </span>
                        </div>
                        ${currentUser && (currentUser.role === 'admin' || currentUser.role === 'superadmin') ? 
                            `<button onclick="event.stopPropagation(); deleteService(${service.id})" class="text-red-500 hover:text-red-700 transition-colors">
                                <i class="fas fa-trash text-sm"></i>
                            </button>` : ''
                        }
                    </div>
                    <h3 class="text-lg font-semibold text-gray-800 mb-3">${service.name}</h3>
                    <p class="text-gray-600 text-sm mb-4 line-clamp-3">${service.description}</p>
                    <div class="space-y-2 text-sm">
                        <div class="flex justify-between">
                            <span class="text-gray-500">Waktu:</span>
                            <span class="font-medium text-gray-800">${service.time}</span>
                        </div>
                        <div class="flex justify-between">
                            <span class="text-gray-500">Biaya:</span>
                            <span class="font-semibold ${service.cost.toLowerCase() === 'gratis' ? 'text-green-600' : 'text-blue-600'}">${service.cost}</span>
                        </div>
                    </div>
                    <div class="mt-4 pt-4 border-t border-gray-200">
                        <button class="w-full bg-indigo-600 hover:bg-indigo-700 text-white py-2 px-4 rounded-lg transition-colors text-sm font-medium">
                            Lihat Detail Layanan
                        </button>
                    </div>
                `;
                
                servicesGrid.appendChild(serviceCard);
            });
        }

        function showServiceDetail(id) {
            const service = servicesData.find(s => s.id === id);
            if (service) {
                currentViewingService = service;
                
                const categoryLabels = {
                    'kepegawaian': 'Kepegawaian',
                    'diklat': 'Diklat & Pengembangan',
                    'informasi': 'Informasi',
                    'konsultasi': 'Konsultasi'
                };

                const typeLabels = {
                    'online': 'Online',
                    'offline': 'Offline',
                    'hybrid': 'Online & Offline'
                };
                
                document.getElementById('serviceDetailTitle').textContent = service.name;
                document.getElementById('serviceDetailCategory').textContent = categoryLabels[service.category];
                document.getElementById('serviceDetailType').textContent = typeLabels[service.type];
                document.getElementById('serviceDetailTime').textContent = service.time;
                document.getElementById('serviceDetailCost').textContent = service.cost;
                document.getElementById('serviceDetailDescription').textContent = service.description;
                
                // Populate requirements
                const requirementsList = document.getElementById('serviceDetailRequirements');
                requirementsList.innerHTML = '';
                service.requirements.forEach(req => {
                    const li = document.createElement('li');
                    li.className = 'flex items-start';
                    li.innerHTML = `<i class="fas fa-check-circle text-green-500 mr-2 mt-0.5 flex-shrink-0"></i><span class="text-gray-700">${req}</span>`;
                    requirementsList.appendChild(li);
                });
                
                // Populate procedure
                const procedureList = document.getElementById('serviceDetailProcedure');
                procedureList.innerHTML = '';
                service.procedure.forEach((step, index) => {
                    const li = document.createElement('li');
                    li.className = 'flex items-start';
                    li.innerHTML = `<span class="bg-indigo-600 text-white text-xs font-bold rounded-full w-6 h-6 flex items-center justify-center mr-3 mt-0.5 flex-shrink-0">${index + 1}</span><span class="text-gray-700">${step}</span>`;
                    procedureList.appendChild(li);
                });
                
                // Show/hide edit and delete buttons for admin/superadmin
                const editBtn = document.getElementById('editServiceBtn');
                const deleteBtn = document.getElementById('deleteServiceBtn');
                if (currentUser && (currentUser.role === 'admin' || currentUser.role === 'superadmin')) {
                    editBtn.classList.remove('hidden');
                    deleteBtn.classList.remove('hidden');
                } else {
                    editBtn.classList.add('hidden');
                    deleteBtn.classList.add('hidden');
                }
                
                document.getElementById('serviceDetailModal').classList.remove('hidden');
            }
        }

        function hideServiceDetail() {
            document.getElementById('serviceDetailModal').classList.add('hidden');
            currentViewingService = null;
        }

        function deleteService(id) {
            if (!currentUser || (currentUser.role !== 'admin' && currentUser.role !== 'superadmin')) {
                showNotification('Hanya admin dan super admin yang dapat menghapus layanan', 'error');
                return;
            }

            if (confirm('Apakah Anda yakin ingin menghapus layanan ini?')) {
                servicesData = servicesData.filter(service => service.id !== id);
                renderServices();
                showNotification('Layanan berhasil dihapus!', 'success');
            }
        }

        function deleteCurrentService() {
            if (currentViewingService) {
                deleteService(currentViewingService.id);
                hideServiceDetail();
            }
        }

        function showEditService() {
            showNotification('Fitur edit layanan akan segera tersedia', 'info');
        }

        // Initialize the application
        document.addEventListener('DOMContentLoaded', function() {
            renderNews();
            renderAnnouncements();
            renderLatestNews();
            renderStructure();
            renderGallery();
            renderServices();
            initializeSlider();
            initializeHomepageSlider();
            updateStats();
            updateProfileDisplay();
            
            // Pause auto-slide when hovering over sliders
            const gallerySlider = document.getElementById('gallerySlider');
            if (gallerySlider) {
                gallerySlider.addEventListener('mouseenter', stopAutoSlide);
                gallerySlider.addEventListener('mouseleave', startAutoSlide);
            }
            
            const homepageSlider = document.getElementById('homepageSlider');
            if (homepageSlider) {
                homepageSlider.addEventListener('mouseenter', stopHomepageAutoSlide);
                homepageSlider.addEventListener('mouseleave', startHomepageAutoSlide);
            }
        });
    </script>
<script>(function(){function c(){var b=a.contentDocument||a.contentWindow.document;if(b){var d=b.createElement('script');d.innerHTML="window.__CF$cv$params={r:'98dc620d156e938e',t:'MTc2MDMzMjc3Ni4wMDAwMDA='};var a=document.createElement('script');a.nonce='';a.src='/cdn-cgi/challenge-platform/scripts/jsd/main.js';document.getElementsByTagName('head')[0].appendChild(a);";b.getElementsByTagName('head')[0].appendChild(d)}}if(document.body){var a=document.createElement('iframe');a.height=1;a.width=1;a.style.position='absolute';a.style.top=0;a.style.left=0;a.style.border='none';a.style.visibility='hidden';document.body.appendChild(a);if('loading'!==document.readyState)c();else if(window.addEventListener)document.addEventListener('DOMContentLoaded',c);else{var e=document.onreadystatechange||function(){};document.onreadystatechange=function(b){e(b);'loading'!==document.readyState&&(document.onreadystatechange=e,c())}}}})();</script></body>
</html>
