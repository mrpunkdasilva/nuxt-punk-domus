<template>
  <main class="tech-docs-page">
    <header class="tech-docs-header">
      <div class="header-content">
        <h1>Tech Docs</h1>
        <p class="section-description">
          Documentações técnicas detalhadas sobre arquitetura, padrões e implementações
        </p>
        <!-- Barra de busca -->
        <div class="search-bar">
          <i class="fas fa-search"></i>
          <input
            type="text"
            v-model="searchQuery"
            placeholder="Buscar documentação..."
            @input="filterDocs"
          >
        </div>
      </div>
      <!-- Efeito decorativo cyberpunk -->
      <div class="cyber-lines">
        <div class="line"></div>
        <div class="line"></div>
        <div class="line"></div>
      </div>
    </header>

    <div class="tech-docs-grid">
      <!-- Análises Técnicas -->
      <section class="docs-section analysis" @mouseenter="activateGlow($event)" @mouseleave="deactivateGlow($event)">
        <div class="section-icon">
          <i class="fas fa-microscope"></i>
        </div>
        <h2>Análises Técnicas</h2>
        <ul>
          <li>Decisões de Arquitetura</li>
          <li>Soluções Complexas</li>
          <li>Comparativos de Tecnologias</li>
          <li>Performance e Otimizações</li>
        </ul>
        <div class="section-footer">
          <span class="doc-count">12 docs</span>
          <button class="view-all">Ver todos <i class="fas fa-arrow-right"></i></button>
        </div>
      </section>

      <!-- Arquitetura & Design -->
      <section class="docs-section architecture" @mouseenter="activateGlow($event)" @mouseleave="deactivateGlow($event)">
        <div class="section-icon">
          <i class="fas fa-layer-group"></i>
        </div>
        <h2>Arquitetura & Design</h2>
        <ul>
          <li>Padrões Arquiteturais</li>
          <li>Design Patterns</li>
          <li>Microservices</li>
          <li>APIs & Databases</li>
        </ul>
        <div class="section-footer">
          <span class="doc-count">15 docs</span>
          <button class="view-all">Ver todos <i class="fas fa-arrow-right"></i></button>
        </div>
      </section>

      <!-- Code Analysis -->
      <section class="docs-section code" @mouseenter="activateGlow($event)" @mouseleave="deactivateGlow($event)">
        <div class="section-icon">
          <i class="fas fa-code"></i>
        </div>
        <h2>Análise de Código</h2>
        <ul>
          <li>Refatorações</li>
          <li>Clean Code</li>
          <li>Boas Práticas</li>
          <li>Code Reviews</li>
        </ul>
        <div class="section-footer">
          <span class="doc-count">8 docs</span>
          <button class="view-all">Ver todos <i class="fas fa-arrow-right"></i></button>
        </div>
      </section>

      <!-- Engineering -->
      <section class="docs-section engineering" @mouseenter="activateGlow($event)" @mouseleave="deactivateGlow($event)">
        <div class="section-icon">
          <i class="fas fa-cogs"></i>
        </div>
        <h2>Engenharia</h2>
        <ul>
          <li>Fundamentos Teóricos</li>
          <li>Algoritmos</li>
          <li>Estruturas de Dados</li>
          <li>Otimização</li>
        </ul>
        <div class="section-footer">
          <span class="doc-count">10 docs</span>
          <button class="view-all">Ver todos <i class="fas fa-arrow-right"></i></button>
        </div>
      </section>
    </div>

    <!-- Featured Docs -->
    <section class="featured-docs">
      <h2>Documentações em Destaque</h2>
      <div class="docs-cards">
        <article v-for="doc in featuredDocs" :key="doc.id" class="doc-card">
          <div class="card-header">
            <i :class="doc.icon"></i>
            <span class="category">{{ doc.category }}</span>
          </div>
          <h3>{{ doc.title }}</h3>
          <p>{{ doc.description }}</p>
          <div class="card-footer">
            <span class="date">{{ doc.date }}</span>
            <button class="read-more">Ler mais</button>
          </div>
        </article>
      </div>
    </section>

    <!-- Latest Updates -->
    <section class="latest-updates">
      <h2>Últimas Atualizações</h2>
      <div class="updates-timeline">
        <div v-for="update in latestUpdates" :key="update.id" class="update-item">
          <div class="update-date">{{ update.date }}</div>
          <div class="update-content">
            <span class="update-tag" :class="update.type">{{ update.type }}</span>
            <h3>{{ update.title }}</h3>
            <p>{{ update.description }}</p>
            <div class="update-meta">
              <span class="author"><i class="fas fa-user"></i> {{ update.author }}</span>
              <span class="category"><i class="fas fa-folder"></i> {{ update.category }}</span>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Tech Categories -->
    <section class="tech-categories">
      <h2>Categorias</h2>
      <div class="categories-grid">
        <div v-for="category in techCategories" :key="category.id" class="category-card">
          <div class="category-icon">
            <i :class="category.icon"></i>
          </div>
          <h3>{{ category.name }}</h3>
          <p>{{ category.count }} documentos</p>
          <div class="category-tags">
            <span v-for="tag in category.tags" :key="tag" class="tag">{{ tag }}</span>
          </div>
        </div>
      </div>
    </section>

    <!-- Quick Access -->
    <section class="quick-access">
      <h2>Acesso Rápido</h2>
      <div class="quick-links">
        <a v-for="link in quickLinks" :key="link.id" :href="link.url" class="quick-link">
          <i :class="link.icon"></i>
          <span>{{ link.title }}</span>
          <span class="link-description">{{ link.description }}</span>
        </a>
      </div>
    </section>
  </main>
</template>

<script>
export default {
  name: 'TechDocs',
  data() {
    return {
      searchQuery: '',
      featuredDocs: [
        {
          id: 1,
          title: 'Clean Architecture em Microserviços',
          description: 'Implementando Clean Architecture em um ambiente de microserviços com Node.js',
          category: 'Arquitetura',
          icon: 'fas fa-layer-group',
          date: '2024-02-15'
        },
        {
          id: 2,
          title: 'Otimização de Performance React',
          description: 'Técnicas avançadas de otimização para aplicações React de larga escala',
          category: 'Performance',
          icon: 'fas fa-tachometer-alt',
          date: '2024-02-10'
        },
        {
          id: 3,
          title: 'Design Patterns em TypeScript',
          description: 'Implementação prática dos principais padrões de projeto usando TypeScript',
          category: 'Patterns',
          icon: 'fas fa-code',
          date: '2024-02-05'
        }
      ],
      latestUpdates: [
        {
          id: 1,
          date: '2024-02-20',
          type: 'new',
          title: 'Guia de Deploy com Docker',
          description: 'Nova documentação sobre práticas de deploy usando Docker e Docker Compose',
          author: 'João Silva',
          category: 'DevOps'
        },
        {
          id: 2,
          date: '2024-02-18',
          type: 'update',
          title: 'Atualização: Clean Architecture',
          description: 'Adicionadas novas seções sobre casos de uso e adaptadores',
          author: 'Maria Santos',
          category: 'Arquitetura'
        },
        {
          id: 3,
          date: '2024-02-15',
          type: 'fix',
          title: 'Correção: Tutorial GraphQL',
          description: 'Corrigidos exemplos de mutations e atualizadas as dependências',
          author: 'Pedro Costa',
          category: 'Backend'
        }
      ],
      techCategories: [
        {
          id: 1,
          name: 'Frontend',
          icon: 'fas fa-laptop-code',
          count: 25,
          tags: ['React', 'Vue', 'Angular', 'CSS']
        },
        {
          id: 2,
          name: 'Backend',
          icon: 'fas fa-server',
          count: 30,
          tags: ['Node.js', 'Python', 'Java', 'API']
        },
        {
          id: 3,
          name: 'DevOps',
          icon: 'fas fa-network-wired',
          count: 18,
          tags: ['Docker', 'K8s', 'CI/CD', 'AWS']
        },
        {
          id: 4,
          name: 'Mobile',
          icon: 'fas fa-mobile-alt',
          count: 15,
          tags: ['React Native', 'Flutter', 'iOS', 'Android']
        }
      ],
      quickLinks: [
        {
          id: 1,
          title: 'Guia de Contribuição',
          description: 'Como contribuir com a documentação',
          icon: 'fas fa-hands-helping',
          url: '/contribute'
        },
        {
          id: 2,
          title: 'Templates',
          description: 'Templates para novos documentos',
          icon: 'fas fa-file-alt',
          url: '/templates'
        },
        {
          id: 3,
          title: 'FAQ',
          description: 'Perguntas frequentes',
          icon: 'fas fa-question-circle',
          url: '/faq'
        }
      ]
    }
  },
  methods: {
    filterDocs() {
      // Implementar lógica de busca
      console.log('Filtering docs:', this.searchQuery)
    },
    activateGlow(event) {
      event.currentTarget.classList.add('glow-active')
    },
    deactivateGlow(event) {
      event.currentTarget.classList.remove('glow-active')
    }
  },
  head() {
    return {
      title: 'Tech Docs - PunkDomus',
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: 'Documentações técnicas detalhadas sobre arquitetura, padrões e implementações'
        }
      ]
    }
  }
}
</script>

<style scoped>
.tech-docs-page {
    min-height: 100vh;
    height: 100%;
    width: 100%;
    background: linear-gradient(180deg,
    rgba(8, 14, 26, 0.9) 0%,
    rgba(8, 14, 26, 0.95) 50%,
    rgba(8, 14, 26, 0.9) 100%
  );
    padding: 5rem 3rem;
    padding-bottom: 9rem;
}

.tech-docs-header {
  text-align: center;
  margin-bottom: 60px;
  position: relative;
  justify-content: center;
}

.header-content {
  position: relative;
  z-index: 2;
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
}

.cyber-lines {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  overflow: hidden;
  z-index: 1;
}

.cyber-lines .line {
  position: absolute;
  height: 2px;
  background: linear-gradient(90deg, transparent, #21DEEA, transparent);
  animation: cyber-line 8s infinite;
  opacity: 0.3;
}

.cyber-lines .line:nth-child(1) {
  top: 20%;
  width: 80%;
  left: 10%;
  animation-delay: 0s;
}

.cyber-lines .line:nth-child(2) {
  top: 40%;
  width: 60%;
  left: 20%;
  animation-delay: 2s;
}

.cyber-lines .line:nth-child(3) {
  top: 60%;
  width: 70%;
  left: 15%;
  animation-delay: 4s;
}

@keyframes cyber-line {
  0% { transform: translateX(-100%); }
  100% { transform: translateX(100%); }
}

.tech-docs-header h1 {
  font-size: 3.5em;
  color: #21DEEA;
  text-transform: uppercase;
  margin-bottom: 20px;
  font-family: 'Protest Guerrilla', sans-serif;
  text-shadow:
    0 0 10px rgba(33, 222, 234, 0.5),
    0 0 20px rgba(33, 222, 234, 0.3);
}

.search-bar {
  max-width: 500px;
  margin: 30px auto 0;
  position: relative;
}

.search-bar input {
  width: 100%;
  padding: 12px 40px;
  background: rgba(8, 14, 26, 0.8);
  border: 1px solid rgba(33, 222, 234, 0.3);
  border-radius: 25px;
  color: #fff;
  font-size: 1.1em;
  transition: all 0.3s ease;
}

.search-bar input:focus {
  outline: none;
  border-color: #21DEEA;
  box-shadow: 0 0 15px rgba(33, 222, 234, 0.3);
}

.search-bar i {
  position: absolute;
  left: 15px;
  top: 50%;
  transform: translateY(-50%);
  color: #21DEEA;
}

.section-description {
  font-size: 1.2em;
  color: #FC5D7F;
  max-width: 800px;
  margin: 0 auto;
  line-height: 1.6;
}

.tech-docs-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 30px;
  margin: 40px 0;
}

.docs-section {
  padding: 30px;
  background: rgba(8, 14, 26, 0.8);
  border-radius: 15px;
  border: 1px solid rgba(33, 222, 234, 0.2);
  transition: all 0.3s ease;
  position: relative;
  overflow: hidden;
}

.docs-section::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: linear-gradient(45deg, transparent, rgba(33, 222, 234, 0.1), transparent);
  transform: translateX(-100%);
  transition: transform 0.6s ease;
}

.docs-section.glow-active::before {
  transform: translateX(100%);
}

.docs-section:hover {
  transform: translateY(-5px);
  border-color: #21DEEA;
  box-shadow: 0 0 20px rgba(33, 222, 234, 0.2);
}

.section-icon {
  font-size: 2em;
  color: #21DEEA;
  margin-bottom: 20px;
  text-align: center;
}

.docs-section h2 {
  color: #FC5D7F;
  font-size: 1.5em;
  margin-bottom: 20px;
  text-align: center;
}

.docs-section ul {
  list-style: none;
  padding: 0;
  margin-bottom: 20px;
}

.docs-section ul li {
  color: #fff;
  margin: 10px 0;
  padding-left: 20px;
  position: relative;
}

.docs-section ul li::before {
  content: '→';
  position: absolute;
  left: 0;
  color: #FC5D7F;
}

.section-footer {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-top: 20px;
  padding-top: 20px;
  border-top: 1px solid rgba(33, 222, 234, 0.2);
}

.doc-count {
  color: #21DEEA;
  font-size: 0.9em;
}

.view-all {
  background: none;
  border: none;
  color: #FC5D7F;
  cursor: pointer;
  display: flex;
  align-items: center;
  gap: 8px;
  font-size: 0.9em;
  transition: all 0.3s ease;
}

.view-all:hover {
  color: #21DEEA;
}

.view-all i {
  transition: transform 0.3s ease;
}

.view-all:hover i {
  transform: translateX(5px);
}

.featured-docs {
  margin-top: 80px;
}

.featured-docs h2 {
  font-size: 2em;
  color: #21DEEA;
  margin-bottom: 30px;
  text-align: center;
}

.docs-cards {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 30px;
}

.doc-card {
  background: rgba(8, 14, 26, 0.8);
  border: 1px solid rgba(33, 222, 234, 0.2);
  border-radius: 15px;
  padding: 25px;
  transition: all 0.3s ease;
}

.doc-card:hover {
  transform: translateY(-5px);
  border-color: #21DEEA;
  box-shadow: 0 0 20px rgba(33, 222, 234, 0.2);
}

.card-header {
  display: flex;
  align-items: center;
  gap: 10px;
  margin-bottom: 15px;
}

.card-header i {
  color: #21DEEA;
  font-size: 1.2em;
}

.category {
  color: #FC5D7F;
  font-size: 0.9em;
}

.doc-card h3 {
  color: #21DEEA;
  font-size: 1.3em;
  margin-bottom: 10px;
}

.doc-card p {
  color: #fff;
  font-size: 0.95em;
  margin-bottom: 20px;
  line-height: 1.5;
}

.card-footer {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-top: auto;
}

.date {
  color: #FC5D7F;
  font-size: 0.85em;
}

.read-more {
  background: none;
  border: 1px solid #21DEEA;
  color: #21DEEA;
  padding: 5px 15px;
  border-radius: 20px;
  cursor: pointer;
  transition: all 0.3s ease;
}

.read-more:hover {
  background: #21DEEA;
  color: #080E1A;
}

.latest-updates {
  margin-top: 60px;
  padding: 30px;
  background: rgba(8, 14, 26, 0.8);
  border-radius: 15px;
}

.updates-timeline {
  margin-top: 30px;
}

.update-item {
  display: flex;
  gap: 20px;
  padding: 20px;
  border-left: 2px solid #21DEEA;
  margin-bottom: 20px;
  background: rgba(33, 222, 234, 0.05);
  border-radius: 0 15px 15px 0;
}

.update-date {
  color: #21DEEA;
  font-size: 0.9em;
  min-width: 100px;
}

.update-tag {
  display: inline-block;
  padding: 3px 8px;
  border-radius: 12px;
  font-size: 0.8em;
  margin-bottom: 10px;
}

.update-tag.new {
  background: rgba(0, 255, 0, 0.2);
  color: #4CAF50;
}

.update-tag.update {
  background: rgba(33, 222, 234, 0.2);
  color: #21DEEA;
}

.update-tag.fix {
  background: rgba(255, 87, 34, 0.2);
  color: #FF5722;
}

.update-content h3 {
  color: #FC5D7F;
  margin-bottom: 8px;
}

.update-meta {
  margin-top: 10px;
  display: flex;
  gap: 20px;
  color: #21DEEA;
  font-size: 0.9em;
}

.tech-categories {
  margin-top: 60px;
}

.categories-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 20px;
  margin-top: 30px;
}

.category-card {
  background: rgba(8, 14, 26, 0.8);
  border: 1px solid rgba(33, 222, 234, 0.2);
  border-radius: 15px;
  padding: 20px;
  text-align: center;
  transition: all 0.3s ease;
}

.category-card:hover {
  transform: translateY(-5px);
  border-color: #21DEEA;
  box-shadow: 0 0 20px rgba(33, 222, 234, 0.2);
}

.category-icon {
  font-size: 2em;
  color: #21DEEA;
  margin-bottom: 15px;
}

.category-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
  margin-top: 15px;
  justify-content: center;
}

.tag {
  background: rgba(252, 93, 127, 0.1);
  color: #FC5D7F;
  padding: 3px 8px;
  border-radius: 12px;
  font-size: 0.8em;
}

.quick-access {
  margin-top: 60px;
  margin-bottom: 60px;
}

.quick-links {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 20px;
  margin-top: 30px;
}

.quick-link {
  display: flex;
  align-items: center;
  gap: 15px;
  padding: 20px;
  background: rgba(8, 14, 26, 0.8);
  border: 1px solid rgba(33, 222, 234, 0.2);
  border-radius: 15px;
  text-decoration: none;
  color: #fff;
  transition: all 0.3s ease;
}

.quick-link:hover {
  transform: translateX(5px);
  border-color: #21DEEA;
  background: rgba(33, 222, 234, 0.1);
}

.quick-link i {
  font-size: 1.5em;
  color: #21DEEA;
}

.quick-link span {
  display: block;
}

.link-description {
  font-size: 0.9em;
  color: #FC5D7F;
  margin-top: 5px;
}

@media (max-width: 768px) {
  .tech-docs-page {
    padding: 60px 15px;
  }

  .tech-docs-header h1 {
    font-size: 2.5em;
  }

  .section-description {
    font-size: 1em;
  }

  .tech-docs-grid {
    grid-template-columns: 1fr;
  }

  .docs-cards {
    grid-template-columns: 1fr;
  }

  .update-item {
    flex-direction: column;
    gap: 10px;
  }

  .update-date {
    min-width: auto;
  }

  .quick-links {
    grid-template-columns: 1fr;
  }
}
</style>
