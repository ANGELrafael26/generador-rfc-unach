<script setup>
import { ref, computed } from 'vue';
import InputText from 'primevue/inputtext';
import Button from 'primevue/button';

// Control del Menú y Módulo Activo
const menuOpen = ref(true);
const toggleMenu = () => {
  menuOpen.value = !menuOpen.value;
};

const moduloActivo = ref('Demo Clientes');

const cambiarModulo = (nombreModulo) => {
  moduloActivo.value = nombreModulo;
};

// Formulario y Gafete
const nombre = ref('Angel');
const apellidoPaterno = ref('Gutierrez');
const apellidoMaterno = ref('Castro');
const fechaNacimiento = ref('11/06/2003');
const rfcGenerado = ref('GUCA030611XXX');

const tarjetaData = ref({
  nombre: 'ANGEL',
  apellidos: 'GUTIERREZ CASTRO',
  puesto: 'Empleado VIP',
  rfc: 'GUCA030611XXX'
});

const generarTarjeta = () => {
  tarjetaData.value = {
    nombre: nombre.value.toUpperCase(),
    apellidos: `${apellidoPaterno.value} ${apellidoMaterno.value}`.toUpperCase(),
    puesto: 'Empleado VIP',
    rfc: rfcGenerado.value.toUpperCase()
  };
};

// Patrón de barras dinámico por RFC
const patronBarras = computed(() => {
  const rfc = tarjetaData.value.rfc || 'DEFAULT';
  const barras = [];
  barras.push(4, 1, 3);
  for (let i = 0; i < rfc.length; i++) {
    const charCode = rfc.charCodeAt(i);
    const anchoBarra1 = (charCode % 5) + 1;
    const anchoEspacio = ((charCode * 3) % 3) + 1;
    const anchoBarra2 = ((charCode * 7) % 5) + 1;
    barras.push(anchoBarra1, anchoEspacio, anchoBarra2);
  }
  barras.push(2, 1, 5);
  return barras;
});

// Elementos del Menú con SVGs Inline Integrados
const menuModulos = [
  { 
    label: 'Demo Clientes', 
    svg: '<path d="M19 3H5c-1.1 0-2 .9-2 2v14c0 1.1.9 2 2 2h14c1.1 0 2-.9 2-2V5c0-1.1-.9-2-2-2zm-7 3c1.66 0 3 1.34 3 3s-1.34 3-3 3-3-1.34-3-3 1.34-3 3-3zm6 12H6v-1c0-2 4-3.1 6-3.1s6 1.1 6 3.1v1z"/>'
  },
  { 
    label: 'BarCode-QR', 
    svg: '<path d="M19 3H5c-1.1 0-2 .9-2 2v14c0 1.1.9 2 2 2h14c1.1 0 2-.9 2-2V5c0-1.1-.9-2-2-2zm-7 3c1.66 0 3 1.34 3 3s-1.34 3-3 3-3-1.34-3-3 1.34-3 3-3zm6 12H6v-1c0-2 4-3.1 6-3.1s6 1.1 6 3.1v1z"/>'
  },
  { 
    label: 'Empleados', 
    svg: '<path d="M19 3H5c-1.1 0-2 .9-2 2v14c0 1.1.9 2 2 2h14c1.1 0 2-.9 2-2V5c0-1.1-.9-2-2-2zm-7 3c1.66 0 3 1.34 3 3s-1.34 3-3 3-3-1.34-3-3 1.34-3 3-3zm6 12H6v-1c0-2 4-3.1 6-3.1s6 1.1 6 3.1v1z"/>'
  },
  { 
    label: 'Graficas', 
    svg: '<path d="M5 9.2h3V19H5zM10.6 5h2.8v14h-2.8zm5.6 8H19v6h-2.8z"/>'
  },
  { 
    label: 'Input', 
    svg: '<path d="M19 3H5c-1.1 0-2 .9-2 2v14c0 1.1.9 2 2 2h14c1.1 0 2-.9 2-2V5c0-1.1-.9-2-2-2zm-9 14l-5-5 1.41-1.41L10 14.17l7.59-7.59L19 8l-9 9z"/>'
  },
  { 
    label: 'Float Label', 
    svg: '<path d="M17 3H7c-1.1 0-1.99.9-1.99 2L5 21l7-3 7 3V5c0-1.1-.9-2-2-2z"/>'
  },
  { 
    label: 'Invalid State', 
    svg: '<path d="M12 2C6.48 2 2 6.48 2 12s4.48 10 10 10 10-4.48 10-10S17.52 2 12 2zm1 15h-2v-2h2v2zm0-4h-2V7h2v6z"/>'
  },
  { 
    label: 'Button', 
    svg: '<path d="M17 1.01L7 1c-1.1 0-2 .9-2 2v18c0 1.1.9 2 2 2h10c1.1 0 2-.9 2-2V3c0-1.1-.9-1.99-2-1.99zM17 19H7V5h10v14z"/>'
  },
  { 
    label: 'Table', 
    svg: '<path d="M4 4h16c1.1 0 2 .9 2 2v12c0 1.1-.9 2-2 2H4c-1.1 0-2-.9-2-2V6c0-1.1.9-2 2-2zm0 4h7v4H4V8zm9 0h7v4h-7V8zm-9 6h7v4H4v-4zm9 0h7v4h-7v-4z"/>'
  },
  { 
    label: 'List', 
    svg: '<path d="M3 13h2v-2H3v2zm0 4h2v-2H3v2zm0-8h2V7H3v2zm4 4h14v-2H7v2zm0 4h14v-2H7v2zM7 7v2h14V7H7z"/>'
  },
  { 
    label: 'Tree', 
    svg: '<path d="M18 16.08c-.76 0-1.44.3-1.96.77L8.91 12.7c.05-.23.09-.46.09-.7s-.04-.47-.09-.7l7.05-4.11c.54.5 1.25.81 2.04.81 1.66 0 3-1.34 3-3s-1.34-3-3-3-3 1.34-3 3c0 .24.04.47.09.7L8.04 9.81C7.5 9.31 6.79 9 6 9c-1.66 0-3 1.34-3 3s1.34 3 3 3c.79 0 1.5-.31 2.04-.81l7.12 4.16c-.05.21-.08.43-.08.65 0 1.61 1.31 2.92 2.92 2.92s2.92-1.31 2.92-2.92c0-1.61-1.31-2.92-2.92-2.92z"/>'
  },
  { 
    label: 'Panel', 
    svg: '<path d="M19 4H5c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h14c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 14H5V8h14v10z"/>'
  }
];
</script>

<template>
  <div style="min-height: 100vh; background-color: #090a0f; color: #f8fafc; font-family: 'Segoe UI', system-ui, -apple-system, sans-serif; display: flex; flex-direction: column;">
    
    <!-- BARRA SUPERIOR (TOPBAR) -->
    <header style="height: 65px; background: #111319; border-bottom: 1px solid #2a2e3d; display: flex; align-items: center; padding: 0 1.5rem; justify-content: space-between; position: sticky; top: 0; z-index: 100;">
      <div style="display: flex; align-items: center; gap: 1.25rem;">
        <button @click="toggleMenu" style="background: transparent; border: none; color: #cbd5e1; font-size: 1.4rem; cursor: pointer; display: flex; align-items: center; justify-content: center; width: 38px; height: 38px; border-radius: 8px;">
          ☰
        </button>

        <div style="display: flex; align-items: center; gap: 0.75rem;">
          <div style="width: 35px; height: 35px; border-radius: 50%; border: 2px solid #cbd5e1; display: flex; align-items: center; justify-content: center; font-weight: 900; font-size: 0.75rem; color: #e2e8f0; background: #161922;">
            U
          </div>
          <div style="display: flex; flex-direction: column;">
            <span style="font-weight: 800; font-size: 1rem; color: #f8fafc; letter-spacing: 0.5px;">Facultad de Negocios</span>
            <span style="font-size: 0.7rem; color: #94a3b8; font-weight: 700; letter-spacing: 1px;">UNACH</span>
          </div>
        </div>
      </div>
    </header>

    <!-- CUERPO PRINCIPAL -->
    <div style="display: flex; flex: 1; overflow: hidden;">
      
      <!-- MENÚ LATERAL (SIDEBAR) -->
      <aside 
        :style="{
          width: menuOpen ? '260px' : '0px',
          opacity: menuOpen ? 1 : 0,
          padding: menuOpen ? '1.5rem 1rem' : '0px',
          overflowY: 'auto',
          transition: 'all 0.3s ease',
          background: '#0d0e12',
          borderRight: menuOpen ? '1px solid #2a2e3d' : 'none',
          boxSizing: 'border-box'
        }"
      >
        <div v-if="menuOpen">
          <div style="font-size: 0.7rem; font-weight: 800; color: #64748b; text-transform: uppercase; letter-spacing: 1px; margin-bottom: 0.75rem;">
            UNIVERSIDAD AUTÓNOMA DE CHIAPAS
          </div>

          <!-- Opción Dashboard con Icono Casa SVG -->
          <div 
            @click="cambiarModulo('Dashboard')"
            :style="{
              display: 'flex',
              alignItems: 'center',
              gap: '0.75rem',
              padding: '0.65rem 0.8rem',
              borderRadius: '8px',
              background: moduloActivo === 'Dashboard' ? '#1e222d' : '#161922',
              color: moduloActivo === 'Dashboard' ? '#38bdf8' : '#e2e8f0',
              fontWeight: '700',
              marginBottom: '1.5rem',
              border: '1px solid #2a2e3d',
              cursor: 'pointer'
            }"
          >
            <svg style="width: 20px; height: 20px; fill: currentColor;" viewBox="0 0 24 24">
              <path d="M10 20v-6h4v6h5v-8h3L12 3 2 12h3v8z"/>
            </svg>
            <span style="font-size: 0.9rem;">Dashboard</span>
          </div>

          <div style="font-size: 0.7rem; font-weight: 800; color: #64748b; text-transform: uppercase; letter-spacing: 1px; margin-bottom: 0.75rem;">
            MÓDULOS
          </div>

          <!-- Opciones Módulos con SVGs -->
          <nav style="display: flex; flex-direction: column; gap: 0.3rem;">
            <div 
              v-for="(item, index) in menuModulos" 
              :key="index"
              @click="cambiarModulo(item.label)"
              :style="{
                display: 'flex',
                alignItems: 'center',
                gap: '0.75rem',
                padding: '0.6rem 0.8rem',
                borderRadius: '8px',
                background: (moduloActivo === item.label) ? '#1e222d' : 'transparent',
                color: (moduloActivo === item.label) ? '#38bdf8' : '#94a3b8',
                fontSize: '0.875rem',
                fontWeight: '600',
                cursor: 'pointer'
              }"
            >
              <svg style="width: 18px; height: 18px; fill: currentColor; flex-shrink: 0;" viewBox="0 0 24 24" v-html="item.svg"></svg>
              <span>{{ item.label }}</span>
            </div>
          </nav>
        </div>
      </aside>

      <!-- ÁREA DE CONTENIDO PRINCIPAL -->
      <main style="flex: 1; padding: 2rem; overflow-y: auto;">
        
        <!-- Módulo Generador RFC / Tarjeta Digital -->
        <div v-if="moduloActivo === 'Demo Clientes' || moduloActivo === 'BarCode-QR'" style="display: flex; gap: 2rem; flex-wrap: wrap; justify-content: center; align-items: flex-start;">
          
          <!-- Formulario -->
          <div style="flex: 1; max-width: 460px; min-width: 300px; background: linear-gradient(145deg, #161922, #0d0e12); padding: 2rem; border-radius: 16px; border: 1px solid #2a2e3d; box-shadow: 0 15px 35px rgba(0,0,0,0.6);">
            <h3 style="margin-top: 0; font-size: 1.1rem; font-weight: 800; color: #e2e8f0; text-transform: uppercase; letter-spacing: 1.5px; border-bottom: 2px solid #333a4d; padding-bottom: 0.75rem;">
              GENERAR EL RFC DE UNA PERSONA
            </h3>
            
            <div style="display: flex; flex-direction: column; gap: 1rem; margin-top: 1.25rem;">
              <div>
                <label style="display: block; font-size: 0.75rem; font-weight: 700; margin-bottom: 0.35rem; color: #94a3b8; text-transform: uppercase; letter-spacing: 0.8px;">Nombre(s):</label>
                <InputText v-model="nombre" style="width: 100%; background: #090a0f; border: 1px solid #333a4d; color: #f8fafc; padding: 0.6rem 0.8rem; border-radius: 8px;" placeholder="Nombre(s)" />
              </div>

              <div>
                <label style="display: block; font-size: 0.75rem; font-weight: 700; margin-bottom: 0.35rem; color: #94a3b8; text-transform: uppercase; letter-spacing: 0.8px;">Apellido Paterno:</label>
                <InputText v-model="apellidoPaterno" style="width: 100%; background: #090a0f; border: 1px solid #333a4d; color: #f8fafc; padding: 0.6rem 0.8rem; border-radius: 8px;" placeholder="Apellido Paterno" />
              </div>

              <div>
                <label style="display: block; font-size: 0.75rem; font-weight: 700; margin-bottom: 0.35rem; color: #94a3b8; text-transform: uppercase; letter-spacing: 0.8px;">Apellido Materno:</label>
                <InputText v-model="apellidoMaterno" style="width: 100%; background: #090a0f; border: 1px solid #333a4d; color: #f8fafc; padding: 0.6rem 0.8rem; border-radius: 8px;" placeholder="Apellido Materno" />
              </div>

              <div>
                <label style="display: block; font-size: 0.75rem; font-weight: 700; margin-bottom: 0.35rem; color: #94a3b8; text-transform: uppercase; letter-spacing: 0.8px;">Fecha Nacimiento:</label>
                <InputText v-model="fechaNacimiento" style="width: 100%; background: #090a0f; border: 1px solid #333a4d; color: #f8fafc; padding: 0.6rem 0.8rem; border-radius: 8px;" placeholder="DD/MM/AAAA" />
              </div>

              <div>
                <label style="display: block; font-size: 0.75rem; font-weight: 700; margin-bottom: 0.35rem; color: #94a3b8; text-transform: uppercase; letter-spacing: 0.8px;">RFC:</label>
                <InputText v-model="rfcGenerado" style="width: 100%; background: #090a0f; border: 1px solid #333a4d; color: #f8fafc; padding: 0.6rem 0.8rem; border-radius: 8px;" placeholder="RFC" />
              </div>

              <div style="margin-top: 0.5rem;">
                <Button label="GENERAR" style="width: 100%; background: linear-gradient(135deg, #e2e8f0 0%, #94a3b8 50%, #64748b 100%); color: #0f172a; border: none; font-weight: 800; padding: 0.75rem; border-radius: 8px; letter-spacing: 1px; cursor: pointer; box-shadow: 0 4px 15px rgba(226, 232, 240, 0.2);" @click="generarTarjeta" />
              </div>
            </div>
          </div>

          <!-- Tarjeta Digital Gafete VIP -->
          <div style="flex: 1; max-width: 460px; min-width: 300px; background: linear-gradient(145deg, #161922, #0d0e12); padding: 2rem; border-radius: 16px; border: 1px solid #2a2e3d; box-shadow: 0 15px 35px rgba(0,0,0,0.6); display: flex; flex-direction: column; align-items: center;">
            <h3 style="margin-top: 0; font-size: 1.1rem; font-weight: 800; color: #e2e8f0; text-transform: uppercase; letter-spacing: 1.5px; border-bottom: 2px solid #333a4d; padding-bottom: 0.75rem; width: 100%;">
              TARJETA DIGITAL
            </h3>
            
            <div style="width: 290px; background: linear-gradient(180deg, #111319 0%, #1a1d26 100%); border-radius: 20px; overflow: hidden; box-shadow: 0 20px 40px rgba(0, 0, 0, 0.9); border: 1px solid #383e52; margin-top: 1rem;">
              
              <div style="padding: 1.25rem 1rem 0.75rem 1rem; text-align: center; background: linear-gradient(90deg, #1e222d 0%, #2a2f3d 50%, #1e222d 100%); border-bottom: 1px solid #383e52;">
                <div style="color: #f1f5f9; font-weight: 900; letter-spacing: 3px; font-size: 0.85rem; text-transform: uppercase;">YOUR COMPANY</div>
                <div style="color: #94a3b8; font-size: 0.65rem; text-transform: uppercase; margin-top: 2px; letter-spacing: 1.5px;">Slogan Goes Here</div>
              </div>

              <div style="display: flex; justify-content: center; margin: 1.5rem 0 1rem 0;">
                <div style="width: 90px; height: 90px; border-radius: 50%; background: linear-gradient(135deg, #333a4d, #0f172a); display: flex; align-items: center; justify-content: center; border: 3px solid #cbd5e1; box-shadow: 0 0 20px rgba(203, 213, 225, 0.25);">
                  <svg style="width: 48px; height: 48px; fill: #e2e8f0;" viewBox="0 0 24 24">
                    <path d="M12 12c2.21 0 4-1.79 4-4s-1.79-4-4-4-4 1.79-4 4 1.79 4 4 4zm0 2c-2.67 0-8 1.34-8 4v2h16v-2c0-2.66-5.33-4-8-4z"/>
                  </svg>
                </div>
              </div>

              <div style="padding: 0.5rem 1rem 1.25rem 1rem; text-align: center;">
                <div style="font-weight: 900; font-size: 1.2rem; text-transform: uppercase; color: #f8fafc; letter-spacing: 0.5px;">{{ tarjetaData.nombre }}</div>
                <div style="font-weight: 900; font-size: 1.2rem; text-transform: uppercase; color: #f8fafc; margin-bottom: 0.25rem; letter-spacing: 0.5px;">{{ tarjetaData.apellidos }}</div>
                <div style="font-size: 0.8rem; color: #94a3b8; font-weight: 600; margin-bottom: 1rem; letter-spacing: 1px; text-transform: uppercase;">{{ tarjetaData.puesto }}</div>

                <div style="display: inline-block; background: #090a0f; padding: 0.4rem 1.1rem; border-radius: 20px; border: 1px solid #333a4d; font-size: 0.8rem; font-weight: 800; color: #cbd5e1; margin-bottom: 1.25rem; letter-spacing: 1px;">
                  ID : {{ tarjetaData.rfc }}
                </div>

                <!-- Código de barras Dinámico por RFC -->
                <div style="display: flex; flex-direction: column; align-items: center; background: #ffffff; padding: 0.65rem; border-radius: 10px;">
                  <div style="display: flex; gap: 2px; height: 35px; align-items: center; max-width: 210px; overflow: hidden;">
                    <div 
                      v-for="(ancho, index) in patronBarras" 
                      :key="index"
                      :style="{
                        width: ancho + 'px',
                        height: '100%',
                        backgroundColor: index % 2 === 0 ? '#0f172a' : 'transparent'
                      }"
                    ></div>
                  </div>
                  <div style="font-size: 0.65rem; color: #334155; font-family: monospace; margin-top: 5px; letter-spacing: 2px; font-weight: bold;">
                    {{ tarjetaData.rfc }}
                  </div>
                </div>
              </div>

              <div style="height: 6px; background: linear-gradient(90deg, #94a3b8, #f8fafc, #64748b);"></div>
            </div>
          </div>

        </div>

        <!-- Vista para el Módulo Dashboard -->
<div v-else-if="moduloActivo === 'Dashboard'" style="display: flex; flex-direction: column; gap: 2rem;">
  
  <!-- Tarjetas KPI -->
  <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(220px, 1fr)); gap: 1.5rem;">
    <div style="background: linear-gradient(145deg, #161922, #0d0e12); padding: 1.5rem; border-radius: 12px; border: 1px solid #2a2e3d;">
      <div style="color: #94a3b8; font-size: 0.8rem; font-weight: 700; text-transform: uppercase;">Total Clientes</div>
      <div style="color: #f8fafc; font-size: 1.8rem; font-weight: 900; margin-top: 0.5rem;">1,248</div>
    </div>
    
    <div style="background: linear-gradient(145deg, #161922, #0d0e12); padding: 1.5rem; border-radius: 12px; border: 1px solid #2a2e3d;">
      <div style="color: #94a3b8; font-size: 0.8rem; font-weight: 700; text-transform: uppercase;">RFCs Generados Hoy</div>
      <div style="color: #38bdf8; font-size: 1.8rem; font-weight: 900; margin-top: 0.5rem;">42</div>
    </div>

    <div style="background: linear-gradient(145deg, #161922, #0d0e12); padding: 1.5rem; border-radius: 12px; border: 1px solid #2a2e3d;">
      <div style="color: #94a3b8; font-size: 0.8rem; font-weight: 700; text-transform: uppercase;">Gafetes VIP Activos</div>
      <div style="color: #e2e8f0; font-size: 1.8rem; font-weight: 900; margin-top: 0.5rem;">890</div>
    </div>
  </div>

  <!-- Acceso Rápido al Módulo principal -->
  <div style="background: linear-gradient(145deg, #161922, #0d0e12); padding: 2rem; border-radius: 16px; border: 1px solid #2a2e3d; text-align: center;">
    <h3 style="color: #f8fafc; margin-top: 0;">Módulo RFC & Gafete Digital</h3>
    <p style="color: #94a3b8; max-width: 500px; margin: 0 auto 1.5rem auto;">
      Accede directamente al generador de RFC y previsualizador de código de barras para clientes.
    </p>
    <Button label="IR A DEMO CLIENTES" style="background: linear-gradient(135deg, #e2e8f0 0%, #94a3b8 50%, #64748b 100%); color: #0f172a; border: none; font-weight: 800; padding: 0.75rem 2rem; border-radius: 8px; cursor: pointer;" @click="cambiarModulo('Demo Clientes')" />
  </div>

</div>

      </main>
    </div>
  </div>
</template>