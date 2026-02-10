import React, { useState } from 'react';
import { CheckCircle, XCircle, Users, Calendar, MapPin, Smartphone, ShieldCheck, LogOut, User, Phone, Home, Mail, Ticket } from 'lucide-react';

// --- CONFIGURACIÓN TEATRO ---
const TOTAL_CAPACITY = 50;
const EVENT_DATE = "Sábado 21 de Octubre, 21:00 HS";
const EVENT_LOCATION = "Teatro Gran Rex - Av. Corrientes 857";
const PLAY_NAME = "El Fantasma de la Ópera";

// --- VISTAS (COMPONENTES EXTERNOS PARA EVITAR ERRORES DE FOCO) ---

// 1. Vista de Registro (Pública - Taquilla Virtual)
const RegistrationView = ({ seatsLeft, totalCapacity, formData, setFormData, handleRegister, setView }) => (
  <div className="max-w-md mx-auto bg-white rounded-xl shadow-2xl overflow-hidden md:max-w-2xl m-4 border-t-4 border-red-800">
    <div className="bg-red-900 p-8 text-white text-center relative overflow-hidden">
      {/* Efecto de telón de fondo */}
      <div className="absolute top-0 left-0 w-full h-full bg-black opacity-20"></div>
      <div className="relative z-10">
        <h1 className="text-3xl font-serif font-bold tracking-wider mb-1">{PLAY_NAME}</h1>
        <p className="text-red-200 text-sm uppercase tracking-widest">Venta de Entradas Anticipadas</p>
      </div>
    </div>
    
    <div className="p-6">
      <div className="flex items-center justify-between bg-red-50 p-4 rounded-lg mb-6 border border-red-100">
        <div className="flex items-center text-red-900">
          <Ticket size={20} className="mr-2" />
          <span className="font-semibold text-sm uppercase">Butacas Libres:</span>
        </div>
        <span className={`text-2xl font-bold ${seatsLeft < 10 ? 'text-red-600 animate-pulse' : 'text-gray-800'}`}>
          {seatsLeft} / {totalCapacity}
        </span>
      </div>

      {seatsLeft > 0 ? (
        <form onSubmit={handleRegister} className="space-y-4">
          {/* Nombre y DNI */}
          <div className="grid grid-cols-1 gap-4">
            <div>
              <label className="block text-gray-700 text-xs font-bold mb-1 flex items-center">
                <User size={14} className="mr-1"/> Nombre del Espectador
              </label>
              <input 
                required
                type="text" 
                className="w-full px-3 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-red-500 text-sm"
                placeholder="Ej: María González"
                value={formData.name}
                onChange={e => setFormData({...formData, name: e.target.value})}
              />
            </div>
            <div>
              <label className="block text-gray-700 text-xs font-bold mb-1 flex items-center">
                <ShieldCheck size={14} className="mr-1"/> DNI (Para validar ingreso)
              </label>
              <input 
                required
                type="number" 
                className="w-full px-3 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-red-500 text-sm"
                placeholder="Sin puntos"
                value={formData.dni}
                onChange={e => setFormData({...formData, dni: e.target.value})}
              />
            </div>
          </div>

          {/* Edad y Teléfono */}
          <div className="grid grid-cols-2 gap-4">
            <div>
              <label className="block text-gray-700 text-xs font-bold mb-1">Edad</label>
              <input 
                required
                type="number" 
                className="w-full px-3 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-red-500 text-sm"
                placeholder="Ej: 28"
                value={formData.age}
                onChange={e => setFormData({...formData, age: e.target.value})}
              />
            </div>
            <div>
              <label className="block text-gray-700 text-xs font-bold mb-1 flex items-center">
                <Phone size={14} className="mr-1"/> Celular
              </label>
              <input 
                required
                type="tel" 
                className="w-full px-3 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-red-500 text-sm"
                placeholder="WhatsApp"
                value={formData.phone}
                onChange={e => setFormData({...formData, phone: e.target.value})}
              />
            </div>
          </div>

          {/* Dirección / Barrio */}
          <div>
            <label className="block text-gray-700 text-xs font-bold mb-1 flex items-center">
              <Home size={14} className="mr-1"/> Ciudad / Localidad
            </label>
            <input 
              required
              type="text" 
              className="w-full px-3 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-red-500 text-sm"
              placeholder="Ej: Capital Federal"
              value={formData.address}
              onChange={e => setFormData({...formData, address: e.target.value})}
            />
          </div>

           {/* Email (Opcional) */}
           <div>
            <label className="block text-gray-700 text-xs font-bold mb-1 flex items-center">
              <Mail size={14} className="mr-1"/> Email (Para enviar comprobante)
            </label>
            <input 
              type="email" 
              className="w-full px-3 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-red-500 text-sm"
              placeholder="correo@ejemplo.com"
              value={formData.email}
              onChange={e => setFormData({...formData, email: e.target.value})}
            />
          </div>

          <button 
            type="submit" 
            className="w-full bg-red-900 text-white font-bold py-3 px-4 rounded-lg hover:bg-black transition duration-300 flex justify-center items-center mt-4 shadow-lg uppercase tracking-wide"
          >
            <Ticket size={20} className="mr-2" />
            Reservar Entrada
          </button>
        </form>
      ) : (
        <div className="text-center p-6 bg-gray-100 rounded-lg border border-gray-300">
          <XCircle size={48} className="text-gray-400 mx-auto mb-2" />
          <h3 className="text-xl font-bold text-gray-700">Función Agotada</h3>
          <p className="text-gray-500">Lo sentimos, no quedan butacas disponibles.</p>
        </div>
      )}
    </div>
    <div className="bg-gray-50 px-8 py-3 text-center border-t border-gray-200">
      <button onClick={() => setView('admin')} className="text-gray-400 text-xs hover:text-red-800 font-semibold">
        (Acceso Staff / Acomodadores)
      </button>
    </div>
  </div>
);

// 2. Vista del Ticket (Éxito)
const TicketView = ({ currentTicket, setView, setFormData }) => (
  <div className="max-w-md mx-auto bg-white rounded-xl shadow-2xl overflow-hidden m-4 border-t-8 border-yellow-500 relative">
    {/* Decoración tipo ticket antiguo */}
    <div className="absolute top-0 right-0 p-4 opacity-10 pointer-events-none">
        <Ticket size={150} />
    </div>

    <div className="p-8 text-center relative z-10">
      <div className="inline-block p-3 rounded-full bg-yellow-100 text-yellow-600 mb-4">
        <CheckCircle size={40} />
      </div>
      <h2 className="text-2xl font-serif font-bold text-gray-900 mb-2">¡Ticket Confirmado!</h2>
      <p className="text-gray-500 mb-6 text-sm">Presenta este código en la entrada del teatro.</p>

      <div className="bg-gray-50 p-6 rounded-xl mb-6 inline-block border-2 border-dashed border-gray-400 relative">
        <img 
          src={`https://api.qrserver.com/v1/create-qr-code/?size=180x180&data=${currentTicket.id}`} 
          alt="QR Code" 
          className="w-40 h-40 mx-auto mix-blend-multiply"
        />
        <p className="text-xs text-gray-500 mt-2 font-mono tracking-widest">ID: {currentTicket.id}</p>
      </div>

      <div className="text-left space-y-3 bg-red-50 p-5 rounded-lg text-sm border-l-4 border-red-800">
        <h3 className="font-bold text-red-900 uppercase mb-2 border-b border-red-200 pb-1">{PLAY_NAME}</h3>
        
        <div className="flex items-center text-gray-700">
          <User size={16} className="mr-3 text-red-800" />
          <span className="font-medium">{currentTicket.name}</span>
        </div>
        <div className="flex items-center text-gray-700">
            <Smartphone size={16} className="mr-3 text-red-800" />
            <span className="font-medium">{currentTicket.dni}</span>
        </div>
        <div className="flex items-center text-gray-700">
          <Calendar size={16} className="mr-3 text-red-800" />
          <span className="font-medium">{EVENT_DATE}</span>
        </div>
        <div className="flex items-center text-gray-700">
          <MapPin size={16} className="mr-3 text-red-800" />
          <span className="font-medium">{EVENT_LOCATION}</span>
        </div>
        <div className="flex items-center text-gray-700 mt-2 pt-2 border-t border-red-200">
           <span className="text-xs text-red-600 font-bold uppercase">Ubicación: General (Por orden de llegada)</span>
        </div>
      </div>

      <div className="mt-8">
          <button 
              onClick={() => {
                  setFormData({ name: '', dni: '', age: '', phone: '', address: '', email: '' });
                  setView('home');
              }}
              className="text-red-800 font-bold hover:underline text-sm uppercase tracking-wide"
          >
              Volver a la Taquilla
          </button>
      </div>
    </div>
  </div>
);

// 3. Vista de Administración (Portero)
const AdminView = ({ setView, handleScan, scanResult, setScanResult, database }) => {
  const [manualInput, setManualInput] = useState('');

  return (
    <div className="max-w-md mx-auto bg-gray-900 text-white min-h-screen p-4">
      <div className="flex justify-between items-center mb-6">
        <h2 className="text-xl font-bold flex items-center text-yellow-500">
          <ShieldCheck className="mr-2" />
          Control de Acceso
        </h2>
        <button onClick={() => setView('home')} className="text-gray-400 hover:text-white">
          <LogOut size={20} />
        </button>
      </div>

      <div className="bg-black rounded-xl p-4 mb-6 border border-gray-800 shadow-xl">
        <div className="aspect-video bg-gray-900 rounded-lg flex items-center justify-center mb-4 relative overflow-hidden">
          <div className="absolute inset-0 border-2 border-red-500 opacity-50 m-8 rounded-lg animate-pulse"></div>
          <span className="text-gray-500 text-sm flex flex-col items-center">
            <Smartphone size={32} className="mb-2 text-gray-600" />
            Cámara de Escaneo
          </span>
        </div>
        
        <div className="flex gap-2">
          <input 
            type="text" 
            placeholder="DNI o ID de Entrada"
            className="flex-1 bg-gray-800 border border-gray-700 rounded px-3 py-2 text-white focus:outline-none focus:border-yellow-500"
            value={manualInput}
            onChange={(e) => setManualInput(e.target.value)}
          />
          <button 
            onClick={() => handleScan(manualInput)}
            className="bg-yellow-600 hover:bg-yellow-700 text-black px-4 py-2 rounded font-bold"
          >
            Validar
          </button>
        </div>
      </div>

      {scanResult && (
        <div className={`p-6 rounded-xl text-center animate-bounce-short mb-6 shadow-2xl border-4 ${
          scanResult.status === 'valid' ? 'bg-green-800 border-green-600' : 
          scanResult.status === 'used' ? 'bg-yellow-700 border-yellow-500' : 'bg-red-800 border-red-600'
        }`}>
          {scanResult.status === 'valid' && (
            <>
              <CheckCircle size={48} className="mx-auto mb-2 text-green-300" />
              <h3 className="text-2xl font-bold text-white">¡ACCESO PERMITIDO!</h3>
              <p className="font-medium text-green-100 text-lg">{scanResult.data.name}</p>
              <p className="text-sm opacity-80 uppercase tracking-widest mt-1">Entrada Válida</p>
            </>
          )}
          {scanResult.status === 'used' && (
            <>
              <XCircle size={48} className="mx-auto mb-2 text-yellow-300" />
              <h3 className="text-2xl font-bold text-white">YA INGRESÓ</h3>
              <p className="text-yellow-100">Este ticket ya fue cortado.</p>
              <p className="text-sm opacity-80 mt-2">Titular: {scanResult.data.name}</p>
            </>
          )}
          {scanResult.status === 'invalid' && (
            <>
              <XCircle size={48} className="mx-auto mb-2 text-red-300" />
              <h3 className="text-2xl font-bold text-white">TICKET INVÁLIDO</h3>
              <p className="text-red-100">No figura en el sistema.</p>
            </>
          )}
          <button 
              onClick={() => { setScanResult(null); setManualInput(''); }}
              className="mt-4 bg-black/40 hover:bg-black/60 px-4 py-2 rounded text-sm w-full font-bold uppercase"
          >
              Escanear Siguiente
          </button>
        </div>
      )}

      <div className="border-t border-gray-800 pt-4">
        <h4 className="text-sm font-bold text-gray-500 mb-3 uppercase tracking-wider">Lista de Invitados ({database.length})</h4>
        <div className="space-y-2 overflow-y-auto max-h-60">
          {database.map((t, idx) => (
            <div key={idx} className="bg-gray-800 p-3 rounded flex justify-between items-center text-xs border-l-2 border-gray-600">
              <div>
                <p className="font-bold text-white">{t.name}</p>
                <p className="text-gray-400">{t.dni}</p>
              </div>
              <span className={`px-2 py-1 rounded font-bold uppercase text-[10px] ${t.status === 'used' ? 'bg-red-900 text-red-200' : 'bg-green-900 text-green-200'}`}>
                {t.status === 'used' ? 'Adentro' : 'Pendiente'}
              </span>
            </div>
          ))}
          {database.length === 0 && <p className="text-gray-700 text-xs text-center italic">La sala está vacía.</p>}
        </div>
      </div>
    </div>
  );
};

// --- COMPONENTE PRINCIPAL ---
export default function App() {
  const [view, setView] = useState('home');
  const [seatsLeft, setSeatsLeft] = useState(TOTAL_CAPACITY);
  
  // Estado ampliado con los nuevos campos
  const [formData, setFormData] = useState({ 
    name: '', 
    dni: '', 
    age: '', 
    phone: '', 
    address: '', 
    email: '' 
  });
  
  const [currentTicket, setCurrentTicket] = useState(null);
  const [scanResult, setScanResult] = useState(null); 
  const [database, setDatabase] = useState([]);

  const handleRegister = (e) => {
    e.preventDefault();
    if (seatsLeft <= 0) return alert("¡Lo sentimos! Se acabaron los cupos.");

    const ticketId = Math.random().toString(36).substr(2, 9).toUpperCase();
    
    const newTicket = {
      id: ticketId,
      ...formData, // Guarda todos los campos nuevos (edad, barrio, etc.)
      status: 'active',
      timestamp: new Date().toISOString()
    };

    setDatabase([...database, newTicket]);
    setSeatsLeft(prev => prev - 1);
    setCurrentTicket(newTicket);
    setView('ticket');
  };

  const handleScan = (input) => {
    const ticket = database.find(t => t.dni === input || t.id === input);

    if (!ticket) {
      setScanResult({ status: 'invalid', data: null });
      return;
    }

    if (ticket.status === 'used') {
      setScanResult({ status: 'used', data: ticket });
      return;
    }

    const updatedDb = database.map(t => 
      t.id === ticket.id ? { ...t, status: 'used' } : t
    );
    setDatabase(updatedDb);
    setScanResult({ status: 'valid', data: ticket });
  };

  return (
    <div className="min-h-screen bg-gray-900 font-sans">
      {view === 'home' && (
        <RegistrationView 
          seatsLeft={seatsLeft} 
          totalCapacity={TOTAL_CAPACITY}
          formData={formData} 
          setFormData={setFormData} 
          handleRegister={handleRegister}
          setView={setView}
        />
      )}
      {view === 'ticket' && (
        <TicketView 
          currentTicket={currentTicket} 
          setView={setView} 
          setFormData={setFormData}
        />
      )}
      {view === 'admin' && (
        <AdminView 
          setView={setView}
          handleScan={handleScan}
          scanResult={scanResult}
          setScanResult={setScanResult}
          database={database}
        />
      )}
    </div>
  );
}