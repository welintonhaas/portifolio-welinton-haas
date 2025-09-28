<template>
  <div class="portfolio">
    <!-- Header -->
    <header class="hero">
      <div class="hero-content">
        <h1 class="hero-name">Welinton Haas</h1>
        <p class="hero-title">Desenvolvedor Full Stack / DevOps</p>
        <p class="hero-description">
          Tech Lead com mais de uma década de experiência transformando desafios de negócio em soluções robustas.
          Especialista em Python, Java, Node.js, DevOps e liderança de equipes de alta performance.
        </p>
        <div class="hero-cta">
          <button @click="scrollToSection('projects')" class="cta-primary">Ver Projetos</button>
          <button @click="scrollToSection('contact')" class="cta-secondary">Contato</button>
        </div>
      </div>
    </header>

    <!-- Skills Section -->
    <section id="skills" class="section skills-section">
      <div class="container">
        <h2 class="section-title">Habilidades Técnicas</h2>
        <div class="skills-grid">
          <div v-for="category in skillCategories" :key="category.name" class="skill-category">
            <h3 class="category-title">{{ category.name }}</h3>
            <div class="skills-list">
              <div v-for="skill in category.skills" :key="skill.name" class="skill-item">
                <div class="skill-info">
                  <span class="skill-name">{{ skill.name }}</span>
                  <span class="skill-level">{{ skill.level }}%</span>
                </div>
                <div class="skill-bar">
                  <div class="skill-progress" :style="{ width: skill.level + '%' }"></div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Projects Section -->
    <section id="projects" class="section projects-section">
      <div class="container">
        <h2 class="section-title">Projetos Desenvolvidos</h2>
        <div class="projects-grid">
          <div v-for="project in projects" :key="project.name" class="project-card">
            <div class="project-header">
              <h3 class="project-title">{{ project.name }}</h3>
              <div class="project-type">{{ project.type }}</div>
            </div>
            <p class="project-description">{{ project.description }}</p>
            <div class="project-tech">
              <span v-for="tech in project.technologies" :key="tech" class="tech-tag">{{ tech }}</span>
            </div>
            <div class="project-actions">
              <a :href="project.url" target="_blank" class="project-link">
                <span>🔗</span> Visitar Site
              </a>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Experience Section -->
    <section id="experience" class="section experience-section">
      <div class="container">
        <h2 class="section-title">Experiência Profissional</h2>
        <div class="timeline">
          <div v-for="exp in experience" :key="exp.id" class="timeline-item">
            <div class="timeline-marker"></div>
            <div class="timeline-content">
              <h3 class="timeline-title">{{ exp.title }}</h3>
              <p class="timeline-period">{{ exp.period }}</p>
              <p class="timeline-description">{{ exp.description }}</p>
              <ul class="timeline-achievements">
                <li v-for="achievement in exp.achievements" :key="achievement">{{ achievement }}</li>
              </ul>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Contact Section -->
    <section id="contact" class="section contact-section">
      <div class="container">
        <h2 class="section-title">Vamos Trabalhar Juntos</h2>
        <div class="contact-content">
          <div class="contact-info">
            <p class="contact-description">
              Interessado em discutir um projeto ou oportunidade? 
              Entre em contato e vamos conversar sobre como posso ajudar.
            </p>
            <div class="contact-links">
              <a href="https://www.linkedin.com/in/welinton-haas/" target="_blank" class="contact-link">
                <span class="contact-icon">💼</span>
                <span>LinkedIn</span>
              </a>
              <a href="https://github.com/welintonhaas" target="_blank" class="contact-link">
                <span class="contact-icon github-icon">
                  <svg viewBox="0 0 16 16" width="24" height="24" fill="currentColor">
                    <path d="M8 0C3.58 0 0 3.58 0 8c0 3.54 2.29 6.53 5.47 7.59.4.07.55-.17.55-.38 0-.19-.01-.82-.01-1.49-2.01.37-2.53-.49-2.69-.94-.09-.23-.48-.94-.82-1.13-.28-.15-.68-.52-.01-.53.63-.01 1.08.58 1.23.82.72 1.21 1.87.87 2.33.66.07-.52.28-.87.51-1.07-1.78-.2-3.64-.89-3.64-3.95 0-.87.31-1.59.82-2.15-.08-.2-.36-1.02.08-2.12 0 0 .67-.21 2.2.82.64-.18 1.32-.27 2-.27.68 0 1.36.09 2 .27 1.53-1.04 2.2-.82 2.2-.82.44 1.1.16 1.92.08 2.12.51.56.82 1.27.82 2.15 0 3.07-1.87 3.75-3.65 3.95.29.25.54.73.54 1.48 0 1.07-.01 1.93-.01 2.2 0 .21.15.46.55.38A8.013 8.013 0 0016 8c0-4.42-3.58-8-8-8z"/>
                  </svg>
                </span>
                <span>GitHub</span>
              </a>
              <a href="mailto:welinton.haas@gmail.com" class="contact-link">
                <span class="contact-icon">📧</span>
                <span>Email</span>
              </a>
            </div>
          </div>
          <div class="contact-form">
            <form @submit.prevent="sendMessage" class="form">
              <div class="form-group">
                <input v-model="contactForm.name" type="text" placeholder="Seu nome" required class="form-input">
              </div>
              <div class="form-group">
                <input v-model="contactForm.email" type="email" placeholder="Seu email" required class="form-input">
              </div>
              <div class="form-group">
                <input v-model="contactForm.subject" type="text" placeholder="Assunto" required class="form-input">
              </div>
              <div class="form-group">
                <textarea v-model="contactForm.message" placeholder="Sua mensagem" required class="form-textarea"></textarea>
              </div>
              <button type="submit" class="form-button" :disabled="isSubmitting">
                {{ isSubmitting ? 'Enviando...' : 'Enviar Mensagem' }}
              </button>
            </form>
          </div>
        </div>
      </div>
    </section>

    <!-- Footer -->
    <footer class="main-footer">
      <div class="container">
        <div class="footer-content">
          <div class="footer-company">
            <h3 class="company-name">WELINTON HAAS DESENVOLVIMENTO DE SOFTWARE LTDA</h3>
            <p class="company-cnpj">CNPJ: 60.431.634/0001-20</p>
          </div>
          <div class="footer-copy">
            <p>&copy; 2025 Welinton Haas. Todos os direitos reservados.</p>
          </div>
        </div>
      </div>
    </footer>
  </div>
</template>

<script setup>
const isSubmitting = ref(false)
const contactForm = ref({
  name: '',
  email: '',
  subject: '',
  message: ''
})

// Dados estruturados do portfólio
const skillCategories = ref([
  {
    name: 'Frontend',
    skills: [
      { name: 'Vue.js', level: 80 },
      { name: 'Angular', level: 85 },
      { name: 'JavaScript ES6+', level: 88 },
      { name: 'HTML5 & CSS3', level: 99 },
      { name: 'TypeScript', level: 90 },
      { name: 'Responsive Design', level: 92 }
    ]
  },
  {
    name: 'Backend & CMS',
    skills: [
      { name: 'Python', level: 88 },
      { name: 'PHP', level: 91 },
      { name: 'Node.js', level: 70 },
      { name: 'Java', level: 93 },
      { name: 'WordPress', level: 90 },
      { name: 'REST APIs', level: 98 }
    ]
  },
  {
    name: 'Ferramentas',
    skills: [
      { name: 'Linux', level: 95 },
      { name: 'Git & GitHub', level: 92 },
      { name: 'Figma', level: 80 },
      { name: 'SEO', level: 85 },
      { name: 'Google Analytics', level: 95 }
    ]
  }
])

const projects = ref([
  {
    name: 'Karina Bogo',
    type: 'Site Institucional',
    description: 'Site profissional para terapeuta especializada em Constelação Familiar com design minimalista e responsivo.',
    technologies: ['WordPress', 'Elementor', 'CSS', 'Responsive Design'],
    url: 'https://karinabogo.com.br'
  },
  {
    name: 'Venah',
    type: ' E-commerce',
    description: 'E-commerce como vitrine virtual dos produtos oferecidos com design moderno.',
    technologies: ['WordPress', 'WooCommerce', 'CSS'],
    url: 'https://venah.com.br'
  },
  {
    name: 'Music Center',
    type: 'E-commerce',
    description: 'Loja online de instrumentos musicais com funcionalidades avançadas de e-commerce.',
    technologies: ['WordPress', 'WooCommerce', 'CSS'],
    url: 'https://lojamusiccenter.com.br'
  },
  {
    name: 'Pizzaria Mais Sabor',
    type: 'Website Comercial',
    description: 'Site para pizzaria e boliche com cardápio online e sistema de eventos.',
    technologies: ['PHP','JavaScript', 'jQuery', 'Google Analytics'],
    url: 'https://www.pizzamaisabor.com.br'
  },
  {
    name: 'Rhaaplex',
    type: 'Site Corporativo',
    description: 'Website para empresa de tecnologia em reciclagem de plásticos flexíveis.',
    technologies: ['Laravel', 'JavaScript', 'Responsive Design', 'Analytics'],
    url: 'https://rhaaplex.com.br'
  },
  {
    name: 'Strike Mídia',
    type: 'Agência Digital',
    description: 'Website para agência de marketing digital e comunicação visual.',
    technologies: ['PHP', 'Design Responsivo','LandingPage'],
    url: 'https://strikemidia.com.br'
  }
])

const experience = ref([
  {
    id: 1,
    title: 'Líder Técnico - Disk & Tenha',
    period: 'abril de 2025 - Presente',
    description: 'Tech Lead responsável por unir liderança de equipe com expertise técnica para impulsionar inovação e eficiência dos projetos.',
    achievements: [
      'Mentoria e direcionamento do time de desenvolvimento',
      'Arquitetura e implementação de novas tecnologias com foco em Clean Architecture',
      'Migração completa da infraestrutura para containers Proxmox e Docker',
      'Aplicação de práticas DevOps para integração e entrega contínua'
    ]
  },
  {
    id: 2,
    title: 'Líder Técnico - Neomind',
    period: 'março de 2023 - abril de 2025',
    description: 'Desenvolvimento de novos projetos desde a escolha das tecnologias até a entrega final, com controle de Sprints e liderança de equipe.',
    achievements: [
      'Controle de Sprints e acompanhamento de progresso da equipe',
      'Code Review e resolução de problemas técnicos',
      'Migração de versão de sistemas garantindo compatibilidade',
      'Treinamento de novos colaboradores e manutenção de aplicações em produção'
    ]
  },
  {
    id: 3,
    title: 'Coordenador Administrativo - IFSC',
    period: 'outubro de 2021 - março de 2023',
    description: 'Gestão de equipe e coordenação do Departamento Administrativo com foco em gestão financeira e projetos.',
    achievements: [
      'Liderança e coordenação de equipe multidisciplinar',
      'Gestão financeira: empenhos, pagamentos e controle orçamentário',
      'Participação em reuniões estratégicas e alinhamento de demandas',
      'Projetos de melhoria da infraestrutura e processos'
    ]
  },
  {
    id: 4,
    title: 'Coordenador de TI - IFSC',
    period: 'janeiro de 2020 - outubro de 2021',
    description: 'Coordenação e supervisão de infraestrutura de TI, incluindo virtualização, redes, segurança e monitoramento de sistemas.',
    achievements: [
      'Administração de containers e VMs em Linux/Windows Server com PROXMOX',
      'Implementação de solução WiFi Fortigate com autenticação FreeRadius',
      'Sistemas de firewall pfSense/OPNSense e monitoramento Zabbix/Grafana',
      'Projeto de Machine Learning para detectar vulnerabilidades em firewall'
    ]
  },
  {
    id: 5,
    title: 'Full Stack Developer - Freelancer',
    period: 'junho de 2019 - junho de 2020',
    description: 'Desenvolvimento web utilizando tecnologias modernas, incluindo aplicação completa para gestão de restaurante.',
    achievements: [
      'Aplicação para gerenciamento de pedidos com Node.js e Angular',
      'Sistema de controle de fluxo de caixa e relatórios estatísticos',
      'Interface responsiva com comunicação direta para cozinha',
      'API Rest, MySQL e versionamento no GitHub'
    ]
  },
  {
    id: 6,
    title: 'Back End Developer - Alfa Transportes',
    period: 'março de 2019 - janeiro de 2020',
    description: 'Desenvolvimento e manutenção de soluções backend, incluindo microserviços Python e aplicações Pascal.',
    achievements: [
      'Microserviço Python para captura e validação de XML de notas fiscais',
      'Desenvolvimento de aplicações internas em Pascal',
      'Melhorias em aplicações web PHP e jQuery',
      'Implantação de sistema RH Senior (HCM) e manipulação PostgreSQL'
    ]
  },
  {
    id: 7,
    title: 'Full Stack Developer - Mz2 Comunicação Visual',
    period: 'novembro de 2015 - dezembro de 2017',
    description: 'Arquiteto de soluções web responsável por todo o ciclo de desenvolvimento, desde concepção visual até implementação final.',
    achievements: [
      'Desenvolvimento de interfaces responsivas com HTML, CSS, Bootstrap e JavaScript',
      'Implementação de lógica de negócio com PHP e autenticação de usuários',
      'Modelagem e gestão de bancos de dados MySQL',
      'Criação de plataformas digitais funcionais e visualmente impactantes'
    ]
  },
  {
    id: 8,
    title: 'Pesquisador Científico - ISEP Portugal',
    period: 'março de 2015 - junho de 2015',
    description: 'Selecionado para programa de pesquisa internacional desenvolvendo instrumentos musicais eletrônicos inovadores.',
    achievements: [
      'Colaboração multidisciplinar com equipe Portugal-Espanha',
      'Desenvolvimento de hardware com Arduino e sensores piezoelétricos',
      'Implementação de sistema de controle e decodificador Java',
      'Projeto apresentado na TV nacional RTP e publicado em revista científica'
    ]
  }
])

// Funções
const scrollToSection = (sectionId) => {
  const element = document.getElementById(sectionId)
  if (element) {
    element.scrollIntoView({ behavior: 'smooth' })
  }
}

const sendMessage = async () => {
  if (!contactForm.value.name || !contactForm.value.email || !contactForm.value.message) {
    alert('Por favor, preencha todos os campos obrigatórios.')
    return
  }

  isSubmitting.value = true
  
  try {
    // Criar dados para envio
    const formData = {
      name: contactForm.value.name,
      email: contactForm.value.email,
      subject: contactForm.value.subject || 'Mensagem do Portfólio',
      message: contactForm.value.message
    }

    // Criar link mailto melhorado
    const subject = encodeURIComponent(formData.subject)
    const body = encodeURIComponent(
`Olá Welinton,

Nome: ${formData.name}
Email: ${formData.email}

Mensagem:
${formData.message}

---
Enviado através do seu portfólio`
    )
    
    const mailtoLink = `mailto:welinton.haas@gmail.com?subject=${subject}&body=${body}`
    
    // Tentar abrir cliente de email
    const mailWindow = window.open(mailtoLink, '_blank')
    
    // Verificar se conseguiu abrir
    setTimeout(() => {
      if (mailWindow && !mailWindow.closed) {
        // Cliente de email abriu com sucesso
        alert('✅ Seu cliente de email foi aberto com a mensagem preenchida!')
        contactForm.value = { name: '', email: '', subject: '', message: '' }
      } else {
        // Fallback para copiar informações
        const contactInfo = `Email: welinton.haas@gmail.com\nAssunto: ${formData.subject}\n\nMensagem:\n${formData.name} (${formData.email})\n${formData.message}`
        
        if (navigator.clipboard) {
          navigator.clipboard.writeText(contactInfo).then(() => {
            alert('📋 Informações copiadas para a área de transferência! Cole em seu cliente de email.')
          }).catch(() => {
            alert('📧 Por favor, envie um email para: welinton.haas@gmail.com')
          })
        } else {
          alert('📧 Por favor, envie um email para: welinton.haas@gmail.com')
        }
        
        contactForm.value = { name: '', email: '', subject: '', message: '' }
      }
    }, 1000)
    
  } catch (error) {
    console.error('Erro ao processar mensagem:', error)
    alert('📧 Por favor, envie um email diretamente para: welinton.haas@gmail.com')
  } finally {
    isSubmitting.value = false
  }
}
</script>

<style scoped>
.portfolio {
  position: relative;
  z-index: 2;
  min-height: 100vh;
}

/* Container */
.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 20px;
}

/* Hero Section */
.hero {
  min-height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  text-align: center;
  background: rgba(255, 255, 255, 0);
  backdrop-filter: blur(0px);
}

.hero-content {
  max-width: 800px;
  padding: 60px 20px;
}

.hero-name {
  font-size: 4rem;
  font-weight: 700;
  margin-bottom: 10px;
  background: linear-gradient(135deg, #FFF, #FFF);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.hero-title {
  font-size: 1.8rem;
  color: #a2ceff;
  margin-bottom: 20px;
  font-weight: 500;
}

.hero-description {
  font-size: 1.2rem;
  color: #fff;
  margin-bottom: 40px;
  line-height: 1.6;
  max-width: 600px;
  margin-left: auto;
  margin-right: auto;
}

.hero-cta {
  display: flex;
  gap: 20px;
  justify-content: center;
  flex-wrap: wrap;
}

.cta-primary, .cta-secondary {
  padding: 15px 30px;
  border-radius: 50px;
  font-weight: 600;
  text-decoration: none;
  transition: all 0.3s ease;
  cursor: pointer;
  border: none;
  font-size: 1rem;
}

.cta-primary {
  background: linear-gradient(135deg, #3b82f6, #1e40af);
  color: white;
}

.cta-primary:hover {
  transform: translateY(-2px);
  box-shadow: 0 10px 25px rgba(59, 130, 246, 0.3);
}

.cta-secondary {
  background: transparent;
  color: #fff;
  border: 2px solid #3b82f6;
}

.cta-secondary:hover {
  background: #3b82f6;
  color: white;
  transform: translateY(-2px);
}

/* Sections */
.section {
  padding: 80px 0;
  background: rgba(255, 255, 255, 1);
  backdrop-filter: blur(8px);
}

.section:nth-child(even) {
  background: rgba(248, 250, 252, 0.95);
}

.section-title {
  font-size: 2.5rem;
  font-weight: 700;
  text-align: center;
  margin-bottom: 60px;
  background: linear-gradient(135deg, #3b82f6, #1e40af);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

/* Skills Section */
.skills-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 40px;
}

.skill-category {
  background: white;
  padding: 30px;
  border-radius: 15px;
  box-shadow: 0 5px 20px rgba(0, 0, 0, 0.1);
  transition: transform 0.3s ease;
}

.skill-category:hover {
  transform: translateY(-5px);
}

.category-title {
  font-size: 1.4rem;
  font-weight: 600;
  margin-bottom: 25px;
  color: #2d3748;
}

.skills-list {
  display: flex;
  flex-direction: column;
  gap: 20px;
}

.skill-item {
  display: flex;
  flex-direction: column;
  gap: 8px;
}

.skill-info {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.skill-name {
  font-weight: 600;
  color: #2d3748;
}

.skill-level {
  font-size: 0.9rem;
  color: #718096;
  font-weight: 500;
}

.skill-bar {
  height: 8px;
  background: #e2e8f0;
  border-radius: 10px;
  overflow: hidden;
}

.skill-progress {
  height: 100%;
  background: linear-gradient(90deg, #3b82f6, #1e40af);
  border-radius: 10px;
  transition: width 1s ease;
}

/* Projects Section */
.projects-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
  gap: 30px;
}

.project-card {
  background: white;
  padding: 30px;
  border-radius: 15px;
  box-shadow: 0 5px 20px rgba(0, 0, 0, 0.1);
  transition: all 0.3s ease;
}

.project-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.15);
}

.project-header {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  margin-bottom: 15px;
}

.project-title {
  font-size: 1.4rem;
  font-weight: 600;
  color: #2d3748;
  margin: 0;
}

.project-type {
  background: linear-gradient(135deg, #3b82f6, #1e40af);
  color: white;
  padding: 5px 12px;
  border-radius: 20px;
  font-size: 0.8rem;
  font-weight: 500;
}

.project-description {
  color: #718096;
  line-height: 1.6;
  margin-bottom: 20px;
}

.project-tech {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
  margin-bottom: 20px;
}

.tech-tag {
  background: #f7fafc;
  color: #4a5568;
  padding: 6px 12px;
  border-radius: 20px;
  font-size: 0.8rem;
  font-weight: 500;
  border: 1px solid #e2e8f0;
}

.project-actions {
  margin-top: auto;
}

.project-link {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  padding: 12px 20px;
  background: linear-gradient(135deg, #3b82f6, #1e40af);
  color: white;
  text-decoration: none;
  border-radius: 25px;
  font-weight: 500;
  transition: all 0.3s ease;
}

.project-link:hover {
  transform: translateY(-2px);
  box-shadow: 0 5px 15px rgba(59, 130, 246, 0.3);
}

/* Experience Section */
.timeline {
  position: relative;
  max-width: 800px;
  margin: 0 auto;
}

.timeline::before {
  content: '';
  position: absolute;
  left: 20px;
  top: 0;
  bottom: 0;
  width: 2px;
  background: linear-gradient(to bottom, #3b82f6, #1e40af);
}

.timeline-item {
  position: relative;
  margin-bottom: 40px;
  padding-left: 60px;
}

.timeline-marker {
  position: absolute;
  left: 11px;
  top: 0;
  width: 18px;
  height: 18px;
  background: linear-gradient(135deg, #3b82f6, #1e40af);
  border-radius: 50%;
  border: 3px solid white;
  box-shadow: 0 0 10px rgba(59, 130, 246, 0.3);
}

.timeline-content {
  background: white;
  padding: 25px;
  border-radius: 15px;
  box-shadow: 0 5px 20px rgba(0, 0, 0, 0.1);
}

.timeline-title {
  font-size: 1.3rem;
  font-weight: 600;
  color: #2d3748;
  margin-bottom: 8px;
}

.timeline-period {
  color: #3b82f6;
  font-weight: 500;
  margin-bottom: 15px;
}

.timeline-description {
  color: #718096;
  line-height: 1.6;
  margin-bottom: 15px;
}

.timeline-achievements {
  list-style: none;
  padding: 0;
}

.timeline-achievements li {
  position: relative;
  padding-left: 20px;
  margin-bottom: 8px;
  color: #4a5568;
}

.timeline-achievements li::before {
  content: '✓';
  position: absolute;
  left: 0;
  color: #3b82f6;
  font-weight: bold;
}

/* Contact Section */
.contact-content {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 60px;
  align-items: start;
}

.contact-description {
  font-size: 1.2rem;
  color: #718096;
  line-height: 1.6;
  margin-bottom: 30px;
}

.contact-links {
  display: flex;
  flex-direction: column;
  gap: 15px;
}

.contact-link {
  display: flex;
  align-items: center;
  gap: 15px;
  padding: 15px 20px;
  background: white;
  border: 2px solid #e2e8f0;
  border-radius: 12px;
  text-decoration: none;
  color: #4a5568;
  font-weight: 500;
  transition: all 0.3s ease;
}

.contact-link:hover {
  border-color: #3b82f6;
  background: #f8faff;
  transform: translateX(5px);
}

.contact-icon {
  font-size: 1.5rem;
}

.github-icon {
  display: flex;
  align-items: center;
  justify-content: center;
}

.github-icon svg {
  transition: transform 0.3s ease;
}

.contact-link:hover .github-icon svg {
  transform: scale(1.1);
}

/* Form Styles */
.form {
  background: white;
  padding: 30px;
  border-radius: 15px;
  box-shadow: 0 5px 20px rgba(0, 0, 0, 0.1);
}

.form-group {
  margin-bottom: 20px;
}

.form-input,
.form-textarea {
  width: 100%;
  padding: 15px;
  border: 2px solid #e2e8f0;
  border-radius: 10px;
  font-size: 1rem;
  transition: all 0.3s ease;
  background: white;
  color: #2d3748;
}

.form-input:focus,
.form-textarea:focus {
  outline: none;
  border-color: #3b82f6;
  box-shadow: 0 0 0 3px rgba(59, 130, 246, 0.1);
}

.form-textarea {
  min-height: 120px;
  resize: vertical;
}

.form-button {
  width: 100%;
  padding: 15px;
  background: linear-gradient(135deg, #3b82f6, #1e40af);
  color: white;
  border: none;
  border-radius: 10px;
  font-size: 1rem;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.3s ease;
}

.form-button:hover:not(:disabled) {
  transform: translateY(-2px);
  box-shadow: 0 5px 15px rgba(59, 130, 246, 0.3);
}

.form-button:disabled {
  opacity: 0.6;
  cursor: not-allowed;
  transform: none;
}

/* Footer */
.main-footer {
  background: linear-gradient(135deg, #1e40af, #1e3a8a);
  color: white;
  padding: 40px 0;
  margin-top: 80px;
}

.footer-content {
  text-align: center;
}

.footer-company {
  margin-bottom: 20px;
}

.company-name {
  font-size: 1.2rem;
  font-weight: 600;
  margin-bottom: 8px;
  color: white;
  letter-spacing: 0.5px;
}

.company-cnpj {
  font-size: 1rem;
  color: rgba(255, 255, 255, 0.8);
  font-family: 'Inter', monospace;
  font-weight: 500;
}

.footer-copy {
  padding-top: 20px;
  border-top: 1px solid rgba(255, 255, 255, 0.2);
}

.footer-copy p {
  color: rgba(255, 255, 255, 0.7);
  font-size: 0.9rem;
  margin: 0;
}

/* Responsive Design */
@media (max-width: 768px) {
  .hero-name {
    font-size: 2.5rem;
  }
  
  .hero-title {
    font-size: 1.4rem;
  }
  
  .hero-description {
    font-size: 1rem;
  }
  
  .hero-cta {
    flex-direction: column;
    align-items: center;
  }
  
  .section-title {
    font-size: 2rem;
  }
  
  .skills-grid,
  .projects-grid {
    grid-template-columns: 1fr;
  }
  
  .contact-content {
    grid-template-columns: 1fr;
    gap: 40px;
  }
  
  .timeline::before {
    left: 15px;
  }
  
  .timeline-item {
    padding-left: 50px;
  }
  
  .timeline-marker {
    left: 6px;
  }
}

@media (max-width: 768px) {
  .company-name {
    font-size: 1rem;
  }
  
  .company-cnpj {
    font-size: 0.9rem;
  }
  
  .main-footer {
    padding: 30px 0;
    margin-top: 60px;
  }
}

@media (max-width: 480px) {
  .container {
    padding: 0 15px;
  }
  
  .hero-name {
    font-size: 2rem;
  }
  
  .company-name {
    font-size: 0.9rem;
    line-height: 1.3;
  }
  
  .company-cnpj {
    font-size: 0.8rem;
  }
  
  .main-footer {
    padding: 25px 0;
    margin-top: 40px;
  }
  
  .section {
    padding: 60px 0;
  }
  
  .skill-category,
  .project-card,
  .timeline-content,
  .form {
    padding: 20px;
  }
}
</style>