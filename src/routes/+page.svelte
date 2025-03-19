<script>
  import { onMount } from 'svelte';
  import { fly } from "svelte/transition";
  import { cubicOut } from "svelte/easing";
  import AOS from 'aos';
  import 'aos/dist/aos.css';

  let isModalOpen = false;
  let isShaking = false;

  const year = new Date().getFullYear();

  const projects = [
    { image: "/project1.png", link: "https://animalclassifier-qz3ik3haivsrjkhnztphxk.streamlit.app/" },
    { image: "/project2.png", link: "https://drive.google.com/file/d/1HZZYoZWhIVOw9qt5ew-H7YslB2LhDPZm/view" },
    { image: "/tagalinis.png", link: "https://drive.google.com/file/d/1IKUMDQKDjRBHMSzqL-Bhyhe2J5lPuWhb/view" },
    { image: "/project3.png", link: "https://drive.google.com/file/d/1bF-DsMObhJMP46L_BrFbMBBH_wE0BREg/view?usp=sharing" }
  ];

  let certifications = [
    { image: "https://www.netacad.com/p/ff9e491c-49be-4734-803e-a79e6e83dab1/badges/badge-images/536abaaf-14d3-4c20-869a-1279dd3a56be.png?response-content-disposition=inlineg",title: "Certification 1", link: "https://drive.google.com/file/d/1yID_e-6zNM5SOsb4J6TkxcnpBZ9f9Rmd/view?usp=sharing" },
    { image: "https://www.netacad.com/p/ff9e491c-49be-4734-803e-a79e6e83dab1/badges/badge-images/d37cd1b7-ce71-45ab-b33d-da7f8ce2a5e2.png?response-content-disposition=inline", title: "Certification 2", link: "https://drive.google.com/file/d/1Ta4J4EoW8dAHlIPHSaBOxNsx5XQe7aJN/view?usp=drive_link" },
    { image: "https://legacy.netacad.com/portal/sites/default/files/badge_template_image/CCNASRWE__1__0.png", title: "Certification 3", link: "https://drive.google.com/file/d/18Bat_Ts-r00A2wsQYFDUGKtO7bhRzTw_/view?usp=sharing" },
    { image: "https://legacy.netacad.com/portal/sites/default/files/badge_template_image/CCNAENSA__1__1.png", title: "Certification 4", link: "https://drive.google.com/file/d/10YwuIgvuDIjf8zraKnGV9C-ZfOwzCBGH/view?usp=sharing" },
    { image: "https://legacy.netacad.com/portal/sites/default/files/badge_template_image/DEVASC_Learning_Badge_0.png", title: "Certification 5", link: "https://drive.google.com/file/d/1djyZCgG8plZEXTmFxWwfr3UlF8egSAIc/view?usp=sharing" },
    { image: "https://www.netacad.com/p/ff9e491c-49be-4734-803e-a79e6e83dab1/badges/badge-images/introduction_to_cybersecurity_16.png", title: "Certification 6", link: "https://drive.google.com/file/d/1O-xiyPEIOl__sSmi5ylPRv03K9GwVuk6/view?usp=sharing" }
  ];

  let startIndex = 0;
  let itemsPerPage = 3; // Show 3 at a time
  let menuOpen = false;

  // Function to toggle the mobile menu
  function toggleMenu() {
    menuOpen = !menuOpen;
  }

  // Function to close the menu on clicking a link
  function closeMenu() {
    menuOpen = false;
  }
  function nextSlide() {
    startIndex = (startIndex + 1) % (certifications.length - (itemsPerPage - 1));
  }

  function prevSlide() {
    startIndex = (startIndex - 1 + (certifications.length - (itemsPerPage - 1))) % (certifications.length - (itemsPerPage - 1));
  }

  function openModal() {
    isModalOpen = true;
    isShaking = true;
    setTimeout(() => isShaking = false, 600); // Remove shake after 600ms
  }
  function closeModal() {
    isModalOpen = false;
  }

  function goToSlide(index) {
  startIndex = index;
}

  // Run this only after the DOM is fully loaded
  onMount(() => {
    
    AOS.init(); // Initialize AOS
    document.querySelectorAll('a[href^="#"]').forEach(anchor => {
      anchor.addEventListener('click', function (e) {
        e.preventDefault();
        document.querySelector(this.getAttribute('href')).scrollIntoView({
          behavior: 'smooth'
        });
      });
    });
  });
</script>

<style>
  @keyframes shake {
      0%, 100% { transform: translateX(0); }
      20% { transform: translateX(-10px); }
      40% { transform: translateX(10px); }
      60% { transform: translateX(-10px); }
      80% { transform: translateX(10px); }
  }

  .shake {
      animation: shake 0.6s ease-in-out;
  }

</style> 

<div
  id="home"
  class="w-full h-screen bg-white overflow-hidden relative flex flex-col items-center"
>
  <!-- Background Image -->
  <img class="w-full h-full absolute top-0 left-0 object-cover" src="bg.jfif" alt="Background" />

<!-- Text Content -->
<div class="absolute top-1/3 text-center px-4 sm:px-6 w-full max-w-[90%] mx-auto">
  <h1 class="text-3xl sm:text-5xl font-semibold text-black">HEY, I’M JAMAL NAGA</h1>
  <h2 class="mt-4 text-2xl sm:text-4xl font-bold text-black leading-snug">
    I aspire to be a <span class="text" style="color: #2563EB;">Network</span> and
    <span class="text" style="color: #2563EB;">Software Engineer</span>,
    and this is my portfolio.
  </h2>
  <p class="text-center mt-4 text-lg sm:text-2xl font-semibold text-black">
    Computer Engineering Student | Web Developer <br />
    Exploring Svelte & Tailwind CSS
  </p>
</div>

<!-- Scroll Indicator -->
<div class="absolute bottom-14 sm:bottom-10 flex justify-center w-full">
  <div
    class="w-8 h-12 sm:w-11 sm:h-16 bg-white border border-3 opacity-80 border-black rounded-full flex justify-center items-center relative overflow-hidden"
  >
    <div
      class="w-[4px] h-[4px] sm:w-[5px] sm:h-[5px] bg-black rounded-full animate-bounce-loop"
    ></div>
  </div>
</div>

<!-- Bounce Animation -->
<style>
  @keyframes bounceLoop {
    0% {
      transform: translateY(-10px);
      opacity: 0;
    }
    50% {
      transform: translateY(10px);
      opacity: 1;
    }
    100% {
      transform: translateY(5px);
      opacity: 0;
    }
  }

  .animate-bounce-loop {
    animation: bounceLoop 1.5s infinite;
  }
</style>


<!-- Navigation Bar -->
<nav
  class="fixed top-0 left-0 w-full h-20 bg-white flex justify-between items-center px-6 md:px-12 shadow-md z-50"
>
  <!-- Logo Section -->
  <div class="flex items-center gap-4 md:gap-5">
    <a href="#home">
      <img
        class="w-12 h-12 md:w-14 md:h-14 rounded-full"
        src="/profile_logo.svg"
        alt="Profile"
      />
    </a>
    <a href="#home">
      <img class="w-28 md:w-36" src="/logo_name.png" alt="Logo" />
    </a>
  </div>

  <!-- Desktop Navigation Links -->
  <div
    class="hidden md:flex gap-4 md:gap-6 text-base md:text-lg font-medium text-black"
  >
    <a href="#home" class="hover:text-purple-500">Home</a>
    <a href="#about" class="hover:text-purple-500">About</a>
    <a href="#projects" class="hover:text-purple-500">Projects</a>
    <a href="#certifications" class="hover:text-purple-500"
      >Certifications</a
    >
  </div>

  <!-- Resume Link (Visible on Desktop) -->
  <a
    href="https://drive.google.com/file/d/1PwFIC1xVFtmNAyUWAoBCzQQHMT3brz6q/view?usp=sharing"
    target="_blank"
    class="hidden md:inline-block px-4 py-2 border border-black rounded-xl text-base md:text-lg font-medium hover:bg-blue-400 hover:text-white"
  >
    My Resume
  </a>

  <!-- Mobile Menu Button -->
  <button
    class="md:hidden text-black focus:outline-none"
    on:click={toggleMenu}
  >
    {#if menuOpen}
      <!-- Close Icon -->
      <svg
        class="w-8 h-8"
        fill="none"
        stroke="currentColor"
        viewBox="0 0 24 24"
        xmlns="http://www.w3.org/2000/svg"
      >
        <path
          stroke-linecap="round"
          stroke-linejoin="round"
          stroke-width="2"
          d="M6 18L18 6M6 6l12 12"
        ></path>
      </svg>
    {:else}
      <!-- Hamburger Icon -->
      <svg
        class="w-8 h-8"
        fill="none"
        stroke="currentColor"
        viewBox="0 0 24 24"
        xmlns="http://www.w3.org/2000/svg"
      >
        <path
          stroke-linecap="round"
          stroke-linejoin="round"
          stroke-width="2"
          d="M4 6h16M4 12h16M4 18h16"
        ></path>
      </svg>
    {/if}
  </button>

  <!-- Mobile Navigation Menu -->
  {#if menuOpen}
    <div
      class="absolute top-20 left-0 w-full bg-white shadow-md flex flex-col items-center gap-4 py-4 md:hidden"
    >
      <a
        href="#home"
        class="text-lg font-medium text-black hover:text-purple-500"
        on:click={closeMenu}
        >Home</a
      >
      <a
        href="#about"
        class="text-lg font-medium text-black hover:text-purple-500"
        on:click={closeMenu}
        >About</a
      >
      <a
        href="#projects"
        class="text-lg font-medium text-black hover:text-purple-500"
        on:click={closeMenu}
        >Projects</a
      >
      <a
        href="#certifications"
        class="text-lg font-medium text-black hover:text-purple-500"
        on:click={closeMenu}
        >Certifications</a
      >
      <a
        href="https://drive.google.com/file/d/1PwFIC1xVFtmNAyUWAoBCzQQHMT3brz6q/view?usp=sharing"
        target="_blank"
        class="px-4 py-2 border border-black rounded-xl text-lg font-medium hover:bg-blue-400 hover:text-white"
        on:click={closeMenu}
      >
        My Resume
      </a>
    </div>
  {/if}
</nav>
</div>


<!-- About Me Section -->
<section id="about" class="w-full min-h-screen bg-[#F1FBFE] flex flex-col items-center px-6 pt-24 pb-12 sm:pt-32 sm:pb-16">
  <h2 class="text-3xl sm:text-5xl font-bold text-black" data-aos="fade-down" data-aos-duration="1200">ABOUT ME</h2>
  <div class="w-12 h-2.5 bg-violet-700 rounded-full mt-2" data-aos="fade-down" data-aos-delay="200"></div>
  <p class="text-base sm:text-lg md:text-2xl text-center max-w-3xl mt-4 px-4 sm:px-0" data-aos="fade-down" data-aos-delay="400">
    Here you will find more information about me, what I do, and my current skills mostly in terms of programming and technology.
  </p>

  <div class="flex flex-col lg:flex-row mt-8 sm:mt-12 w-full max-w-7xl gap-8">
    <!-- Left Section - About Me -->
    <div class="lg:w-1/2 px-4 sm:px-0" data-aos="fade-right" data-aos-easing="ease-in-out" data-aos-duration="1400">
      <h3 class="text-2xl sm:text-3xl font-bold text-black">Get to know me!</h3>
      <p class="mt-4 text-base sm:text-lg leading-relaxed">
        I'm Jamal Naga, a Computer Engineering student exploring web and mobile development. I also have an interest in Cisco networking and robotic automation.
      </p>
      <p class="mt-4 text-base sm:text-lg">
        I'm open to job opportunities where I can contribute, learn, and grow. If you have an opportunity that matches my skills, feel free to contact me.
      </p>

      <button
        class="mt-6 px-6 py-3 text-white bg-purple-500 rounded-md text-lg hover:bg-purple-700 transition"
        on:click={openModal}
        data-aos="zoom-in" data-aos-duration="1000"
      >
        Contact
      </button>
    </div>

    <!-- Right Section - Skills & TechStack -->
    <div class="lg:w-1/2 flex flex-col items-start mt-12 lg:mt-0 px-4 sm:px-0" data-aos="fade-left" data-aos-easing="ease-in-out" data-aos-duration="1400">
      <h3 class="text-2xl sm:text-4xl font-bold text-black">My Skills</h3>
      <div class="grid grid-cols-2 sm:grid-cols-3 gap-2 mt-4">
        {#each ["UI/UX", "Cisco Network", "Robotics", "Web Development", "Mobile Development"] as skill, i}
          <div 
            class="bg-gray-400 text-white px-4 py-2 rounded-md text-sm sm:text-lg text-center"
            data-aos="flip-up"
            data-aos-delay={i * 200} 
            data-aos-duration="1000"
          >
            {skill}
          </div>
        {/each}
      </div>

      <h3 class="text-2xl sm:text-4xl font-bold text-black mt-12">Tech Stack</h3>
      <div class="grid grid-cols-3 sm:grid-cols-4 gap-x-8 sm:gap-x-16 gap-y-6 mt-4">
        {#each [
          { name: "HTML", icon: "/html.svg" },
          { name: "Svelte", icon: "/svelte.svg" },
          { name: "React", icon: "/react.svg" },
          { name: "TailwindCSS", icon: "/tailwindcss.svg" },
          { name: "Firebase", icon: "/firebase.svg" },
          { name: "Python", icon: "/python.svg" },
          { name: "Flask", icon: "/flask.svg" },
          { name: "GitHub", icon: "/github.svg" },
          { name: "Vercel", icon: "/vercel.svg" },
          { name: "Figma", icon: "/figma.svg" },
          { name: "Cisco", icon: "/cisco.svg" },
          { name: "Arduino", icon: "/arduino.svg" }
        ] as tech, i}
          <div class="flex flex-col items-center justify-center"
            data-aos="fade-up"
            data-aos-delay={i * 100}
            data-aos-duration="500"
          >
            <img src={tech.icon} alt={tech.name} class="w-12 sm:w-16 h-12 sm:h-16"/>
            <span class="text-sm sm:text-xl pt-2">{tech.name}</span>
          </div>
        {/each}
      </div>
    </div>
  </div>
</section>


{#if isModalOpen}
  <div class="fixed inset-0 flex items-center justify-center bg-black/50 z-50">
    <div
      class="absolute relative w-[90%] sm:w-[600px] md:w-[700px] lg:w-[809.37px] max-h-[90%] overflow-y-auto bg-white rounded-[10px] p-6 sm:p-8 shadow-lg {isShaking ? 'shake' : ''}"
    >
      <!-- Close Button -->
      <button
        class="absolute top-4 right-4 text-gray-600 text-2xl sm:text-xl"
        on:click={() => (isModalOpen = false)}
      >
        ✕
      </button>

      <!-- Icon -->
      <div class="flex flex-col items-center pt-6 sm:pt-10">
        <img src="Group.svg" alt="Attention Icon" class="w-20 sm:w-24" />
      </div>

      <!-- Modal Title -->
      <h2 class="text-neutral-500 text-3xl sm:text-4xl md:text-5xl font-bold text-center mt-4 sm:mt-6">
        Get In Touch
      </h2>

      <!-- Contact Info -->
      <div
        class="flex flex-col sm:flex-row justify-around mt-8 sm:mt-10 gap-6 sm:gap-0"
      >
        <!-- Address -->
        <div class="text-center">
          <h3 class="text-black text-lg sm:text-xl font-bold">ADDRESS</h3>
          <p class="text-black text-base font-normal">Pinyahan, Quezon City</p>
        </div>

        <!-- Contact -->
        <div class="text-center">
          <h3 class="text-black text-lg sm:text-xl font-bold">CONTACT</h3>
          <p class="text-black text-base font-normal">+639916125691</p>
        </div>

        <!-- Email -->
        <div class="text-center">
          <h3 class="text-black text-lg sm:text-xl font-bold">EMAIL ADDRESS</h3>
          <p class="text-black text-base font-normal">jamal.naga333@gmail.com</p>
        </div>
      </div>
    </div>
  </div>
{/if}


<!-- Projects Section -->
<section id="projects" class="w-full min-h-screen bg-[#EEF7FD] flex flex-col items-center px-6 pt-32 pb-16">
  <h2 class="text-5xl font-bold text-black" data-aos="fade-up" data-aos-duration="1500">PROJECTS</h2>
  <div class="w-12 h-2.5 rounded-full mt-2" style="background-color: #6D28D9;" data-aos="fade-up" data-aos-delay="200"></div>
  <p class="text-lg md:text-2xl text-center max-w-3xl mt-4" data-aos="fade-up" data-aos-delay="400">
    Here are some of the projects I've worked on. Click on them to view more.
  </p>

  <!-- Projects Grid -->
  <div class="grid grid-cols-1 md:grid-cols-2 gap-8 mt-12 w-full max-w-7xl">
    {#each projects as project, i}
      <div 
        class="relative group cursor-pointer overflow-hidden rounded-lg shadow-lg bg-white p-4 project-card"
        data-aos={i % 2 === 0 ? "fade-right" : "fade-left"}
        data-aos-duration="1500"
      >
        <a href={project.link} target="_blank">
          <div class="rounded-lg overflow-hidden shadow-md border border-gray-200">
            <img 
              src={project.image} 
              alt="Preview of project" 
              class="w-full h-[300px] object-cover transition-transform group-hover:scale-105 duration-300"
            />
          </div>
          <div class="absolute inset-0 bg-black/60 opacity-0 group-hover:opacity-100 flex items-center justify-center transition-opacity">
            <span class="text-white text-xl font-bold">View Project</span>
          </div>
      </a>
    </div>
  {/each}
</div>
</section>

<!-- Certification Section -->
<section
  id="certifications"
  class="w-full min-h-screen bg-[#F9F5FD] flex flex-col items-center px-4 sm:px-6 pt-20 sm:pt-32 pb-12 sm:pb-16"
>
  <h2
    class="text-3xl sm:text-5xl font-bold text-black text-center"
    data-aos="fade-up"
    data-aos-duration="1000"
  >
    CERTIFICATIONS
  </h2>
  <div
    class="w-10 sm:w-12 h-2 sm:h-2.5 rounded-full mt-2" style="background-color: #6D28D9;"
    data-aos="fade-up"
    data-aos-delay="200"
  ></div>

  <div
    class="relative w-full max-w-6xl flex items-center mt-8 pl-4 sm:pl-16"
    data-aos="fade-up"
    data-aos-delay="300"
  >
    <!-- Left Button -->
    <button
      on:click={prevSlide}
      class="absolute left-0 bg-gray-500 p-2 sm:p-3 rounded-full text-white hover:bg-gray-700 transition"
      data-aos="fade"
      data-aos-delay="400"
    >
      &#10094;
    </button>

    <!-- Carousel Window -->
    <div class="overflow-hidden w-full max-w-5xl">
      <div
        class="flex transition-transform duration-500 ease-in-out"
        style="transform: translateX(-{startIndex * (100 / itemsPerPage)}%)"
      >
        {#each certifications as cert, i}
        <a
          href={cert.link}
          target="_blank"
          class="flex-shrink-0 w-2/3 sm:w-1/3 px-2 sm:px-3"
          data-aos="zoom-in"
          data-aos-delay="{i * 200}"
        >
          <div
            class="bg-white rounded-xl shadow-lg p-4 sm:p-6 flex flex-col items-center"
          >
            <img
              src={cert.image}
              alt="Certificate"
              class="w-full sm:w-[400px] h-[200px] sm:h-[300px] object-cover rounded-md transition-transform duration-500 hover:scale-105"
            />
            <div
              class="w-32 sm:w-40 p-2 bg-red-600 rounded-md mt-4 sm:mt-6 text-white text-sm sm:text-xl font-bold text-center cursor-pointer hover:bg-red-700 transition"
            >
              View More
            </div>
          </div>
        </a>
        {/each}
      </div>
    </div>

    <!-- Right Button -->
    <button
      on:click={nextSlide}
      class="absolute right-0 bg-gray-500 p-2 sm:p-3 rounded-full text-white hover:bg-gray-700 transition"
      data-aos="fade"
      data-aos-delay="400"
    >
      &#10095;
    </button>
  </div>

  <!-- Dot Indicators -->
  <div class="flex space-x-2 mt-4 sm:mt-6">
    {#each [0, 1, 2, 3] as i}
    <button
      on:click={() => goToSlide(i)}
      aria-label="Go to slide {i + 1}"
      class="w-2.5 sm:w-3 h-2.5 sm:h-3 rounded-full transition-all duration-300"
      style="background-color: {startIndex === i ? '#7C3AED' : '#D1D5DB'}"
    ></button>
    {/each}
  </div>
</section>


<!-- Footer  -->
<footer class="bg-black text-white py-8 px-4 sm:px-6">
  <div
    class="max-w-7xl mx-auto flex flex-col md:flex-row justify-between items-center"
  >
    <!-- Left Section -->
    <div class="text-center md:text-left mb-6 md:mb-0">
      <h2 class="text-lg sm:text-xl font-bold">JAMAL NAGA</h2>
      <p class="text-sm sm:text-base text-gray-400 max-w-xs sm:max-w-md mt-2">
        An aspiring Frontend Web Developer exploring how to build Websites and 
        Mobile applications that contribute to the success of the overall product.
      </p>
    </div>

    <!-- Social Section -->
    <div class="w-full md:w-auto text-center md:text-left">
      <h2 class="text-base sm:text-lg font-bold">SOCIAL</h2>
      <div class="flex justify-center md:justify-start gap-3 sm:gap-4 mt-2">
        <a
          href="https://www.linkedin.com/in/jamal-naga-612049356/"
          target="_blank"
        >
          <img
            src="/linkedin.svg"
            alt="LinkedIn"
            class="w-5 h-5 sm:w-6 sm:h-6 hover:opacity-80 transition"
          />
        </a>
        <a href="https://github.com/jamalmis12" target="_blank">
          <img
            src="/github2.svg"
            alt="GitHub"
            class="w-5 h-5 sm:w-6 sm:h-6 hover:opacity-80 transition"
          />
        </a>
        <a href="https://www.facebook.com/naaaagaaaa/" target="_blank">
          <img
            src="/fb.svg"
            alt="Facebook"
            class="w-5 h-5 sm:w-6 sm:h-6 hover:opacity-80 transition"
          />
        </a>
        <a href="https://www.instagram.com/jaamaal_n/" target="_blank">
          <img
            src="/ig.svg"
            alt="Instagram"
            class="w-5 h-5 sm:w-6 sm:h-6 hover:opacity-80 transition"
          />
        </a>
      </div>
    </div>
  </div>

  <!-- Copyright Section (Centered Below Everything) -->
  <div class="w-full flex flex-col items-center mt-6">
    <div class="border-t w-full max-w-xs sm:max-w-md" style="border-color: #374151;"></div>
    <p class="text-xs sm:text-sm text-gray-500 mt-2 text-center">
      © {new Date().getFullYear()}. Made by
      <span class="font-bold text-white">Jamal Naga</span>
    </p>
  </div>
</footer>

