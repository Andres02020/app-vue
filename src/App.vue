<script setup lang="ts">
import { ref } from 'vue';

// 1. EL CONTRATO (Interface Obligatoria de TypeScript)
interface Producto {
  id: number;
  nombre: string;
  precio: number;
  stock: number;
  categoria: string; // <-- AGREGAMOS ESTO
}

// Estados reactivos para controlar el Login
const isLoggedIn = ref(false);
const username = ref('');
const password = ref('');
const errorMessage = ref('');

// 2. LA COLECCIÓN (Arreglo Fuertemente Tipado bajo la Interface)
const listaProductos = ref<Producto[]>([
  { id: 101, nombre: "Teclado Mecánico RGB", precio: 250, stock: 12, categoria: "Accesorios" },
  { id: 102, nombre: "Mouse Óptico Inalámbrico", precio: 110, stock: 20, categoria: "Accesorios" },
  { id: 103, nombre: "Monitor Gamer 24' 144Hz", precio: 1450, stock: 5, categoria: "Pantallas" }
]);

// Función de control de acceso
const handleLogin = () => {
  if (username.value === 'andres' && password.value === '1234') {
    isLoggedIn.value = true;
    errorMessage.value = '';
  } else {
    errorMessage.value = 'Credenciales Incorrectas. Intente de nuevo.';
  }
};

const handleLogout = () => {
  isLoggedIn.value = false;
  username.value = '';
  password.value = '';
};
</script>

  <template>
  <div class="min-vh-100 min-vw-100 position-fixed top-0 start-0 m-0 p-0 d-flex align-items-center justify-content-center px-3 visual-wrapper" 
       style="background-image: url('https://images.unsplash.com/photo-1518709268805-4e9042af9f23?q=80&w=1920&auto=format&fit=crop'); background-size: cover; background-position: center; font-family: 'Cinzel', 'Segoe UI', serif; z-index: 0;">
    <div class="position-absolute top-0 start-0 w-100 h-100 nordic-overlay"></div>
    
    <div v-if="!isLoggedIn" class="w-100 position-relative" style="max-width: 440px; z-index: 2;">
      <div class="card border-0 shadow-lg text-white god-card">
        
        <div class="text-center py-5 px-4 position-relative card-nordic-header">
          <h2 class="fw-bold tracking-widest text-uppercase mythic-title mb-1">ITPM ALMACÉN</h2>
          <p class="small text-gold tracking-wider mb-0">FORJA DE ACCESORIOS & RUNAS</p>
          <div class="nordic-divider my-3"></div>
        </div>
<div class="text-center my-3">
  <img 
    src="./assets/nordico123.png" 
    alt="Logo Forja Vikinga" 
    style="max-width: 140px; height: auto; filter: drop-shadow(0 0 10px rgba(255, 193, 7, 0.6));"
  />
</div>

        <div class="card-body p-4 p-sm-5 pt-0">
          <form @submit.prevent="handleLogin">
            
            <div class="mb-4">
              <label class="form-label small fw-bold tracking-wide text-gold">IDENTIDAD DEL GUARDIÁN</label>
              <div class="input-group nordic-group">
                <span class="input-group-text border-0 text-gold bg-transparent"><i class="bi bi-shield-shaded"></i></span>
                <input v-model="username" 
                       type="text" 
                       class="form-control bg-transparent text-white border-0 custom-nordic-input" 
                       placeholder="Ej: andres" 
                       required />
              </div>
            </div>

            <div class="mb-4">
              <label class="form-label small fw-bold tracking-wide text-gold">CLAVE DE LA FORJA</label>
              <div class="input-group nordic-group">
                <span class="input-group-text border-0 text-gold bg-transparent"><i class="bi bi-key-fill"></i></span>
                <input v-model="password" 
                       type="password" 
                       class="form-control bg-transparent text-white border-0 custom-nordic-input" 
                       placeholder="••••••••" 
                       required />
              </div>
            </div>
            
            <div v-if="errorMessage" class="alert alert-mythic py-2 text-center small mb-4">
              <i class="bi bi-fire me-2"></i> {{ errorMessage }}
            </div>
            
            <button type="submit" class="btn btn-gold w-100 fw-bold py-2.5 text-uppercase tracking-widest text-dark border-0 transition-all">
              Desbloquear Inventario
            </button>
          </form>
        </div>

        <div class="card-footer text-center py-3 border-0 bg-transparent text-white-50 small">
          <small class="tracking-wide">Protección de Runas TypeScript Activa</small>
        </div>
      </div>
    </div>

    <div v-else class="w-100 position-relative" style="max-width: 650px; z-index: 2;">
      <div class="card border-0 shadow-lg text-white god-card">
        <div class="card-header border-bottom-gold bg-transparent d-flex justify-content-between align-items-center py-4 px-4">
          <h4 class="mb-0 fw-bold tracking-wide text-gold"><i class="bi bi-archive-fill me-2"></i> Inventario de la Forja</h4>
          <button @click="handleLogout" class="btn btn-outline-gold btn-sm px-3 rounded-0 tracking-wider">Cerrar Portal</button>
        </div>
        <div class="card-body p-4 p-sm-5 text-center">
          <h3 class="text-white fw-bold mb-1">¡Bienvenido, Andres Perez!</h3>
          <p class="text-gold small tracking-widest mb-4">CONTROL DE ARTEFACTOS EN TIEMPO REAL</p>
          
          <div class="nordic-divider my-3"></div>
          
          <ul class="list-group list-group-flush text-start bg-transparent">
            <li v-for="p in listaProductos" :key="p.id" class="list-group-item d-flex justify-content-between align-items-center py-3 bg-transparent text-white border-bottom-dark">
              <div>
                <span class="fw-bold tracking-wide h6 text-white mb-1 d-block">{{ p.nombre }}</span>
                <span class="badge bg-gold text-dark me-2 small px-2 py-1 rounded-0 fw-bold">{{ p.categoria || 'Gamer' }}</span>
                <small class="text-white-50">ID Místico: {{ p.id }}</small>
              </div>
              <span class="badge border border-gold text-gold bg-dark px-3 py-2 rounded-0 fs-6 fw-bold">
                Bs. {{ p.precio }} | {{ p.stock }} pzas.
              </span>
            </li>
          </ul>
        </div>
      </div>
    </div>

  </div>
</template>

<style scoped>
/* Reseteo completo para eliminar las franjas blancas laterales */
:global(html), :global(body), :global(#app) {
  margin: 0 !important;
  padding: 0 !important;
  width: 100% !important;
  height: 100% !important;
  overflow-x: hidden !important;
  background-color: #0a0e16 !important; /* Color oscuro de respaldo si tarda en cargar la foto */
}

.visual-wrapper {
  box-sizing: border-box;
}

.nordic-overlay {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: linear-gradient(135deg, rgba(10, 14, 22, 0.94) 0%, rgba(23, 28, 38, 0.88) 100%);
  z-index: -1; /* Lo enviamos detrás del contenido para que no tape las letras */
}
.visual-wrapper {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.nordic-overlay {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  /* Degradado que simula la niebla de Midgard */
  background: linear-gradient(135deg, rgba(10, 14, 22, 0.94) 0%, rgba(23, 28, 38, 0.88) 100%);
  z-index: 1;
}
/* Fuentes de respaldo místicas */
@import url('https://fonts.googleapis.com/css2?family=Cinzel:wght@500;700;900&display=swap');

.nordic-overlay {
  background: linear-gradient(135deg, rgba(10, 12, 16, 0.92) 0%, rgba(20, 24, 33, 0.85) 100%);
}

/* Tarjeta Estilo Piedra / Ceniza Oscura */
.god-card {
  background: rgba(18, 22, 28, 0.85) !important;
  backdrop-filter: blur(12px);
  -webkit-backdrop-filter: blur(12px);
  border: 1px solid rgba(212, 175, 55, 0.2) !important;
  border-radius: 4px; /* Bordes más rectos y rústicos */
}

.text-gold {
  color: #d4af37 !important; /* Oro Nórdico */
}

.border-bottom-gold {
  border-bottom: 1px solid rgba(212, 175, 55, 0.3) !important;
}

.border-bottom-dark {
  border-bottom: 1px solid rgba(255, 255, 255, 0.1) !important;
}

/* Divisor rúnico simulado */
.nordic-divider {
  height: 2px;
  background: linear-gradient(90deg, transparent 0%, #d4af37 50%, transparent 100%);
  opacity: 0.6;
}

/* Inputs incrustados en la piedra */
.nordic-group {
  background: rgba(0, 0, 0, 0.4);
  border: 1px solid rgba(212, 175, 55, 0.25);
  border-radius: 2px;
}

.custom-nordic-input:focus {
  box-shadow: none !important;
  background-color: rgba(212, 175, 55, 0.05) !important;
}

/* Botón de Oro Nórdico */
.btn-gold {
  background: #d4af37;
  color: #12161c !important;
  font-weight: 900;
  border-radius: 2px;
  letter-spacing: 2px;
}

.btn-gold:hover {
  background: #f1c40f;
  box-shadow: 0 0 15px rgba(212, 175, 55, 0.4);
  transform: translateY(-1px);
}

.btn-outline-gold {
  color: #d4af37;
  border: 1px solid #d4af37;
}

.btn-outline-gold:hover {
  background: #d4af37;
  color: #12161c !important;
}

/* Alerta de Fuego de Muspelheim */
.alert-mythic {
  background: rgba(231, 76, 60, 0.15);
  border: 1px solid rgba(231, 76, 60, 0.4);
  color: #e74c3c;
  border-radius: 2px;
}
</style>