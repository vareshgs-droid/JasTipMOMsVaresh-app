import React, { useState, useMemo, useEffect, useCallback, useRef } from 'react';
import { 
  ShoppingBag, 
  Home, 
  Menu, 
  X, 
  Plus, 
  Trash2, 
  Edit, 
  Save,
  DollarSign,
  User,
  LogOut,
  TrendingUp,
  TrendingDown,
  Database,
  Loader2,
  AlertCircle,
  Plane,
  Calendar,
  MapPin,
  Receipt,
  Calculator,
  Lock,
  UserCheck,
  CheckCircle2,
  ChevronRight,
  FileText,
  Tag,
  Info
} from 'lucide-react';

// ==========================================
// KONFIGURASI GLOBAL
// ==========================================

const USERS = [
  { username: 'superadmin', password: 'spvadmin', role: 'owner', label: 'Direktur/Owner' },
  { username: 'stafed', password: 'staf1', role: 'entry', label: 'Staf Entry Produk' },
  { username: 'staffa', password: 'StafKeu', role: 'finance', label: 'Staf Keuangan' },
];

const DB_CONFIG = { 
  url: 'https://rqsbqpntzofynmudzchm.supabase.co', 
  key: 'sb_publishable_YJ1rZgEZ_8KQ3sOam99u-w_ThOQbVZz' 
};

// ==========================================
// UTILITIES
// ==========================================
const formatRupiah = (val) => {
  const number = Number(val) || 0;
  return 'Rp ' + number.toLocaleString('id-ID');
};

const formatDate = (dateString) => {
  if (!dateString) return '-';
  try {
    const date = new Date(dateString);
    if (isNaN(date.getTime())) return dateString;
    return date.toLocaleDateString('id-ID', { day: 'numeric', month: 'short', year: 'numeric' });
  } catch (e) { return '-'; }
};

// ==========================================
// ATOM COMPONENTS
// ==========================================
const Card = ({ children, className = "" }) => (
  <div className={`bg-white rounded-xl shadow-sm border border-slate-200 overflow-hidden ${className}`}>
    {children}
  </div>
);

const SimpleBarChart = ({ label, value, total, colorClass }) => {
  const safeTotal = Number(total) || 0;
  const safeValue = Number(value) || 0;
  const percentage = safeTotal > 0 ? Math.min(100, Math.round((safeValue / safeTotal) * 100)) : 0;
  return (
    <div className="mb-3">
      <div className="flex justify-between text-[10px] mb-1 font-black text-slate-500 uppercase tracking-widest">
        <span>{label}</span>
        <span>{percentage}%</span>
      </div>
      <div className="w-full bg-slate-100 rounded-full h-2 shadow-inner">
        <div className={`h-2 rounded-full transition-all duration-1000 ${colorClass}`} style={{ width: `${percentage}%` }}></div>
      </div>
    </div>
  );
};

// ==========================================
// MAIN COMPONENT
// ==========================================
export default function App() {
  const isInitialMount = useRef(true);

  // Auth State
  const [isLoggedIn, setIsLoggedIn] = useState(false);
  const [currentUser, setCurrentUser] = useState(null);
  const [loginForm, setLoginForm] = useState({ username: '', password: '' });
  const [loginError, setLoginError] = useState('');

  // UI State
  const [activeTab, setActiveTab] = useState('landing');
  const [activeModule, setActiveModule] = useState('summary');
  const [sidebarOpen, setSidebarOpen] = useState(false);
  const [selectedTripId, setSelectedTripId] = useState(null);
  const [isLoading, setIsLoading] = useState(false);
  const [isSaving, setIsSaving] = useState(false);
  
  // Data State
  const [trips, setTrips] = useState([]);
  const [products, setProducts] = useState([]);
  const [orders, setOrders] = useState([]);
  const [expenses, setExpenses] = useState([]);
  const [isConnected, setIsConnected] = useState(false);

  // Modal State
  const [productModal, setProductModal] = useState({ open: false, type: 'add', data: null });
  const [tripModal, setTripModal] = useState({ open: false, type: 'add', data: null });
  const [financeModal, setFinanceModal] = useState({ open: false, type: 'order', mode: 'add', data: null });
  const [deleteConfirm, setDeleteConfirm] = useState({ open: false, table: '', id: null, label: '' });
  
  // Form State
  const [prodForm, setProdForm] = useState({ name: '', price_buy: 0, fee: 0, image_url: '', description: '' });
  const [tripForm, setTripForm] = useState({ title: '', city: '', status: 'open', date_start: '', date_end: '', deadline: '' });
  const [finForm, setFinForm] = useState({ customer_name: '', total: 0, category: 'Transport', description: '', amount: 0 });

  // --- DATABASE ENGINE ---
  const getHeaders = useCallback(() => ({
    'apikey': DB_CONFIG.key,
    'Authorization': `Bearer ${DB_CONFIG.key}`,
    'Content-Type': 'application/json',
    'Prefer': 'return=representation'
  }), []);

  const fetchData = useCallback(async (silent = false) => {
    if (!DB_CONFIG.url) return;
    if (!silent) setIsLoading(true);
    const headers = getHeaders();
    const baseUrl = DB_CONFIG.url.replace(/\/$/, "");

    try {
      const [resT, resP, resO, resE] = await Promise.all([
        fetch(`${baseUrl}/rest/v1/trips?select=*&order=id.desc`, { headers }),
        fetch(`${baseUrl}/rest/v1/products?select=*&order=id.desc`, { headers }),
        fetch(`${baseUrl}/rest/v1/orders?select=*&order=id.desc`, { headers }),
        fetch(`${baseUrl}/rest/v1/expenses?select=*&order=id.desc`, { headers })
      ]);

      const dataT = resT.ok ? await resT.json() : [];
      const dataP = resP.ok ? await resP.json() : [];
      const dataO = resO.ok ? await resO.json() : [];
      const dataE = resE.ok ? await resE.json() : [];
      
      setTrips(dataT);
      setProducts(dataP.map(p => ({ ...p, image: p.image_url || 'https://placehold.co/400x400?text=No+Image' })));
      setOrders(dataO);
      setExpenses(dataE);

      setSelectedTripId(currentId => {
        if (currentId !== null) return currentId;
        return dataT.length > 0 ? dataT[0].id : -1;
      });

      setIsConnected(true);
    } catch (e) { 
      console.error("Database Fetch Error:", e);
    } finally { 
      if (!silent) setIsLoading(false); 
    }
  }, [getHeaders]);

  useEffect(() => {
    if (isInitialMount.current) {
      fetchData(true);
      isInitialMount.current = false;
    }
  }, [fetchData]);

  // --- AUTH ACTIONS ---
  const handleLogin = (e) => {
    e.preventDefault();
    const user = USERS.find(u => u.username.toLowerCase() === loginForm.username.toLowerCase() && u.password === loginForm.password);
    if (user) {
      setCurrentUser(user);
      setIsLoggedIn(true);
      setActiveTab('dashboard');
      if (user.role === 'entry') setActiveModule('products');
      else if (user.role === 'finance') setActiveModule('finance');
      else setActiveModule('summary');
      setLoginError('');
      setLoginForm({ username: '', password: '' });
    } else {
      setLoginError('Username atau Password salah!');
    }
  };

  const handleLogout = () => {
    setIsLoggedIn(false);
    setCurrentUser(null);
    setActiveTab('landing');
  };

  const supabaseRequest = async (table, method, body, id = null) => {
    setIsSaving(true);
    try {
      let url = `${DB_CONFIG.url}/rest/v1/${table}`;
      if (id) url += `?id=eq.${id}`;
      const res = await fetch(url, { method, headers: getHeaders(), body: body ? JSON.stringify(body) : undefined });
      if (!res.ok) { 
        const err = await res.json(); 
        throw new Error(err.message || "Gagal menghubungi database."); 
      }
      await fetchData(true);
      return true;
    } catch (e) { 
      alert(`Error: ${e.message}`);
      return false; 
    } finally { setIsSaving(false); }
  };

  const handleSaveProduct = async (e) => {
    e.preventDefault();
    if (!selectedTripId || selectedTripId === -1) return alert("Pilih agenda trip dahulu.");
    const payload = {
      name: prodForm.name,
      price_buy: parseInt(prodForm.price_buy) || 0,
      fee: parseInt(prodForm.fee) || 0,
      price_sell: (parseInt(prodForm.price_buy) || 0) + (parseInt(prodForm.fee) || 0),
      image_url: prodForm.image_url || null,
      description: prodForm.description || null,
      trip_id: selectedTripId
    };
    const success = await supabaseRequest('products', productModal.type === 'edit' ? 'PATCH' : 'POST', payload, productModal.data?.id);
    if (success) setProductModal({ ...productModal, open: false });
  };

  const handleSaveTrip = async (e) => {
    e.preventDefault();
    const payload = { ...tripForm, date_start: tripForm.date_start || null, date_end: tripForm.date_end || null, deadline: tripForm.deadline || null };
    const success = await supabaseRequest('trips', tripModal.type === 'edit' ? 'PATCH' : 'POST', payload, tripModal.data?.id);
    if (success) setTripModal({ ...tripModal, open: false });
  };

  const handleSaveFinance = async (e) => {
    e.preventDefault();
    if (!selectedTripId || selectedTripId === -1) return alert("Pilih agenda trip.");
    const isOrder = financeModal.type === 'order';
    const table = isOrder ? 'orders' : 'expenses';
    const body = isOrder 
      ? { customer_name: finForm.customer_name, total: Number(finForm.total), trip_id: selectedTripId, status: 'paid' }
      : { category: finForm.category, description: finForm.description, amount: Number(finForm.amount), trip_id: selectedTripId };
    const success = await supabaseRequest(table, financeModal.mode === 'edit' ? 'PATCH' : 'POST', body, financeModal.data?.id);
    if (success) setFinanceModal({ ...financeModal, open: false });
  };

  const processDelete = async () => {
    const success = await supabaseRequest(deleteConfirm.table, 'DELETE', null, deleteConfirm.id);
    if (success) setDeleteConfirm({ ...deleteConfirm, open: false });
  };

  // --- LOGIKA FILTER DATA ---
  const activeTrip = useMemo(() => trips.find(t => t.id === selectedTripId) || trips[0] || { title: 'Agenda Kosong', city: '-' }, [trips, selectedTripId]);
  const filteredProducts = useMemo(() => products.filter(p => p.trip_id === selectedTripId), [products, selectedTripId]);
  const filteredOrders = useMemo(() => orders.filter(o => o.trip_id === selectedTripId), [orders, selectedTripId]);
  const filteredExpenses = useMemo(() => expenses.filter(e => e.trip_id === selectedTripId), [expenses, selectedTripId]);

  const stats = useMemo(() => {
    const revenue = filteredOrders.reduce((s, o) => s + (Number(o.total) || 0), 0);
    const totalExp = filteredExpenses.reduce((s, e) => s + (Number(e.amount) || 0), 0);
    return { revenue, expenses: totalExp, profit: revenue - totalExp };
  }, [filteredOrders, filteredExpenses]);

  // --- HELPER AKSES & MODAL ---
  const openProdModal = (type, prod = null) => {
    setProductModal({ open: true, type, data: prod });
    if (type === 'edit' && prod) {
      setProdForm({ name: prod.name, price_buy: prod.price_buy, fee: prod.fee || (prod.price_sell - prod.price_buy), image_url: prod.image_url || '', description: prod.description || '' });
    } else {
      setProdForm({ name: '', price_buy: 0, fee: 0, image_url: '', description: '' });
    }
  };

  const openTripModal = (type, trip = null) => {
    setTripModal({ open: true, type, data: trip });
    if (type === 'edit' && trip) {
      setTripForm({ title: trip.title, city: trip.city, status: trip.status || 'open', date_start: trip.date_start || '', date_end: trip.date_end || '', deadline: trip.deadline || '' });
    } else {
      setTripForm({ title: '', city: '', status: 'open', date_start: '', date_end: '', deadline: '' });
    }
  };

  const openFinModal = (type, mode = 'add', data = null) => {
    setFinanceModal({ open: true, type, mode, data });
    if (mode === 'edit' && data) {
      if (type === 'order') setFinForm({ customer_name: data.customer_name, total: data.total });
      else setFinForm({ category: data.category || 'Transport', description: data.description || '', amount: data.amount });
    } else {
      setFinForm({ customer_name: '', total: 0, category: 'Transport', description: '', amount: 0 });
    }
  };

  const confirmDelete = (table, id, label) => {
    setDeleteConfirm({ open: true, table, id, label });
  };

  // ==========================================
  // VIEW: LANDING PAGE (PUBLIK)
  // ==========================================
  if (activeTab === 'landing') {
    return (
      <div className="min-h-screen bg-slate-50 font-sans flex flex-col">
        <nav className="bg-white px-8 py-5 shadow-sm flex justify-between items-center sticky top-0 z-20 border-b border-slate-100">
          <div className="flex items-center gap-3 font-black text-slate-800">
            <div className="bg-emerald-600 p-2.5 rounded-2xl shadow-xl shadow-emerald-100"><ShoppingBag className="text-white" size={24} /></div>
            <span className="tracking-tighter text-2xl uppercase italic">MomsVaresh</span>
          </div>
          <button onClick={() => setActiveTab('dashboard')} className="text-[10px] font-black text-slate-500 hover:text-emerald-600 flex items-center gap-3 bg-slate-50 px-5 py-3 rounded-full border border-slate-200 uppercase tracking-widest transition shadow-sm active:scale-95">
            <User size={16}/> Login Admin
          </button>
        </nav>

        <div className="bg-emerald-600 text-white py-20 px-4 text-center relative overflow-hidden">
          <div className="absolute top-10 left-10 opacity-10 rotate-12"><Plane size={150}/></div>
          <div className="absolute bottom-10 right-10 opacity-10 -rotate-12"><ShoppingBag size={150}/></div>
          <h1 className="text-5xl font-black mb-4 tracking-tighter uppercase italic drop-shadow-xl">Jastip MOMsVARESH</h1>
          <p className="opacity-90 mb-10 text-xl font-medium tracking-tight uppercase">Layanan Jasa Titip Amanah & Terpercaya</p>
          <div className="inline-flex flex-col items-center bg-white/10 backdrop-blur-2xl px-10 py-6 rounded-[2.5rem] border border-white/20 shadow-2xl">
             <span className="text-[10px] uppercase font-black tracking-[0.4em] opacity-60 mb-2">Agenda Jastip Aktif</span>
             <span className="text-2xl font-black tracking-tight uppercase">{activeTrip?.title || 'Menyiapkan Agenda...'}</span>
             <div className="mt-4 flex items-center gap-2 text-[10px] font-black bg-white text-emerald-700 px-6 py-2 rounded-full uppercase tracking-widest">
               <Calendar size={14}/> Batas Order: {formatDate(activeTrip?.deadline)}
             </div>
          </div>
        </div>

        <div className="max-w-7xl mx-auto px-6 py-16 flex-grow">
          <div className="flex flex-col md:flex-row justify-between items-start md:items-end mb-12 gap-8">
             <div>
               <h2 className="text-4xl font-black text-slate-900 tracking-tighter uppercase italic">Katalog Pilihan</h2>
               <p className="text-slate-400 text-sm mt-1 font-bold uppercase tracking-widest opacity-80">Produk terbaik pilihan tim MomsVaresh untuk Anda.</p>
             </div>
             <div className="flex flex-col items-start md:items-end gap-2 w-full md:w-auto">
               <label className="text-[10px] text-slate-400 font-black uppercase tracking-widest ml-1">Pilih Trip</label>
               <select className="w-full md:w-80 text-sm border-2 border-slate-200 rounded-2xl p-4 bg-white shadow-xl font-black text-slate-700 outline-none focus:ring-4 focus:ring-emerald-100 transition cursor-pointer" value={selectedTripId || ''} onChange={e => setSelectedTripId(Number(e.target.value))}>
                  {trips.map(t => <option key={t.id} value={t.id}>{t.title}</option>)}
               </select>
             </div>
          </div>

          <div className="grid grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-10">
            {filteredProducts.map(p => {
              const feeVal = Number(p.fee) || 0;
              const totalVal = Number(p.price_buy) + feeVal;
              return (
              <Card key={p.id} className="flex flex-col h-full hover:shadow-[0_35px_60px_-15px_rgba(0,0,0,0.15)] transition-all duration-500 rounded-[2rem] border-none shadow-xl group relative overflow-hidden">
                <div className="aspect-square bg-slate-100 overflow-hidden relative">
                  <img src={p.image} className="w-full h-full object-cover group-hover:scale-110 transition duration-700" alt={p.name} />
                  <div className="absolute top-4 left-4 bg-white/90 backdrop-blur-md px-3 py-1 rounded-lg text-[9px] font-black text-emerald-600 shadow-sm uppercase tracking-tighter italic">Recommended</div>
                </div>
                <div className="p-6 flex-1 flex flex-col">
                  <div className="font-black text-slate-800 mb-2 leading-tight group-hover:text-emerald-600 transition truncate text-lg uppercase tracking-tighter">{p.name}</div>
                  <div className="text-xs text-slate-400 mb-6 line-clamp-2 min-h-[32px] font-medium leading-relaxed italic opacity-80">{p.description || "Oleh-oleh premium khas perjalanan kami."}</div>
                  <div className="mt-auto pt-6 border-t-2 border-slate-50">
                    <div className="text-[10px] text-slate-400 uppercase font-black tracking-widest mb-1 opacity-60">Harga Barang</div>
                    <div className="text-emerald-700 font-black text-3xl tracking-tighter leading-none italic">{formatRupiah(p.price_buy)}</div>
                    <div className="text-[11px] text-orange-600 font-black mt-4 flex items-center gap-2 bg-orange-50 px-4 py-2 rounded-2xl border border-orange-100/50 w-fit shadow-sm">
                      <Receipt size={14} className="opacity-80" /> + JASTIP {formatRupiah(feeVal)}
                    </div>
                    <a href={`https://wa.me/628567176135?text=Halo MomsVaresh, saya mau titip:%0A*${p.name}*%0A%0ARincian Biaya:%0A- Harga Barang: ${formatRupiah(p.price_buy)}%0A- Fee Jastip: ${formatRupiah(feeVal)}%0A---------------------------%0A*Total Estimasi: ${formatRupiah(totalVal)}*%0A%0AMohon info slotnya yaa 🙏`} target="_blank" rel="noreferrer" className="flex items-center justify-center gap-3 w-full bg-emerald-600 text-white text-[11px] font-black py-5 rounded-2xl mt-6 shadow-2xl hover:bg-emerald-700 active:scale-95 transition uppercase tracking-widest">Pesan Sekarang</a>
                  </div>
                </div>
              </Card>
            )})}
          </div>
          {filteredProducts.length === 0 && (
             <div className="py-32 text-center bg-white rounded-[3rem] border-4 border-dashed border-slate-100 shadow-inner">
               <ShoppingBag className="text-slate-200 mx-auto mb-6" size={64}/>
               <p className="text-slate-400 text-xl font-black uppercase tracking-[0.2em] opacity-50">Katalog Trip Segera Hadir</p>
             </div>
          )}
        </div>

        <footer className="mt-auto py-16 bg-slate-900 text-center px-6 relative overflow-hidden">
          <div className="absolute top-0 right-0 w-64 h-64 bg-emerald-500/5 rounded-full -mr-32 -mt-32"></div>
          <div className="font-black text-white tracking-tighter text-3xl mb-3 uppercase italic">MOMsVARESH</div>
          <p className="text-slate-500 text-[10px] font-black uppercase tracking-[0.4em] mb-10 opacity-70">Jasa Titip Amanah Se-Indonesia • Est 2026</p>
          <div className="grid grid-cols-2 md:grid-cols-4 gap-8 max-w-4xl mx-auto text-white/40 text-[10px] font-black uppercase tracking-widest border-t border-white/5 pt-10">
            <div className="flex flex-col gap-2"><span>Lokasi</span><span className="text-white opacity-80">Indonesia</span></div>
            <div className="flex flex-col gap-2"><span>Jam Operasional</span><span className="text-white opacity-80">24/7 Service</span></div>
            <div className="flex flex-col gap-2"><span>Total Item</span><span className="text-white opacity-80">{products.length} Katalog</span></div>
            <div className="flex flex-col gap-2"><span>Status</span><span className="text-white opacity-80">Online Cloud</span></div>
          </div>
        </footer>
      </div>
    );
  }

  // ==========================================
  // VIEW: ADMIN PANEL
  // ==========================================
  return (
    <div className="flex min-h-screen bg-slate-100 text-slate-800 font-sans">
      <button onClick={() => setSidebarOpen(true)} className="md:hidden fixed top-6 left-6 z-30 bg-white p-3.5 rounded-2xl shadow-2xl border border-slate-200 active:scale-90 transition"><Menu size={24} /></button>

      <div className={`fixed inset-y-0 left-0 bg-slate-900 w-72 text-slate-300 transform ${sidebarOpen ? 'translate-x-0' : '-translate-x-full'} md:translate-x-0 transition-transform z-40 flex flex-col shadow-2xl`}>
        <div className="p-8 border-b border-slate-800/50 bg-slate-900/50">
          <div className="flex items-center gap-4">
             <div className="bg-emerald-600 p-2.5 rounded-2xl shadow-xl shadow-emerald-900/50"><Database size={24} className="text-white"/></div>
             <div className="font-black text-white text-xl tracking-tighter uppercase italic">MomsVaresh Admin</div>
          </div>
          <div className="flex items-center gap-2 mt-6 text-emerald-400 text-[10px] font-black uppercase tracking-widest bg-emerald-400/10 px-4 py-2.5 rounded-xl border border-emerald-400/20">
            <UserCheck size={16}/> {currentUser?.label}
          </div>
        </div>
        
        <nav className="p-6 space-y-3 flex-1 overflow-y-auto">
          {canAccess('summary') && <button onClick={() => { setActiveModule('summary'); setSidebarOpen(false); }} className={`w-full flex items-center gap-4 px-6 py-4 rounded-2xl transition font-black text-xs uppercase tracking-widest ${activeModule === 'summary' ? 'bg-emerald-600 text-white shadow-2xl shadow-emerald-900/50' : 'hover:bg-slate-800'}`}><Home size={20} /> Dashboard</button>}
          {canAccess('trips') && <button onClick={() => { setActiveModule('trips'); setSidebarOpen(false); }} className={`w-full flex items-center gap-4 px-6 py-4 rounded-2xl transition font-black text-xs uppercase tracking-widest ${activeModule === 'trips' ? 'bg-emerald-600 text-white shadow-2xl shadow-emerald-900/50' : 'hover:bg-slate-800'}`}><Plane size={20} /> Agenda Trip</button>}
          {canAccess('products') && <button onClick={() => { setActiveModule('products'); setSidebarOpen(false); }} className={`w-full flex items-center gap-4 px-6 py-4 rounded-2xl transition font-black text-xs uppercase tracking-widest ${activeModule === 'products' ? 'bg-emerald-600 text-white shadow-2xl shadow-emerald-900/50' : 'hover:bg-slate-800'}`}><ShoppingBag size={20} /> Katalog Produk</button>}
          {canAccess('finance') && <button onClick={() => { setActiveModule('finance'); setSidebarOpen(false); }} className={`w-full flex items-center gap-4 px-6 py-4 rounded-2xl transition font-black text-xs uppercase tracking-widest ${activeModule === 'finance' ? 'bg-emerald-600 text-white shadow-2xl shadow-emerald-900/50' : 'hover:bg-slate-800'}`}><DollarSign size={20} /> Keuangan</button>}
        </nav>
        
        <div className="p-8 border-t border-slate-800/50 space-y-4">
          <div className={`flex items-center gap-3 px-4 py-3 rounded-xl border transition-all duration-500 ${isConnected ? 'bg-emerald-500/10 border-emerald-500/20 text-emerald-400' : 'bg-red-500/10 border-red-500/20 text-red-400'}`}>
            <div className={`w-2.5 h-2.5 rounded-full shadow-lg ${isConnected ? 'bg-emerald-500 animate-pulse' : 'bg-red-500'}`}></div>
            <span className="text-[10px] font-black uppercase tracking-widest italic">{isConnected ? 'Cloud Connected' : 'Disconnected'}</span>
          </div>

          <button onClick={handleLogout} className="flex items-center justify-center gap-3 text-red-400 w-full px-6 py-4 hover:bg-red-500/10 rounded-2xl transition font-black text-[10px] border-2 border-red-500/20 active:scale-95 uppercase tracking-widest shadow-lg">
            <LogOut size={18} /> Logout System
          </button>
        </div>
      </div>

      <main className="flex-1 md:ml-72 p-8 md:p-14 overflow-y-auto">
        <div className="flex flex-col md:flex-row justify-between items-start md:items-center mb-14 gap-8">
          <h2 className="text-4xl font-black text-slate-900 uppercase tracking-tighter italic italic">{activeModule}</h2>
          <div className="bg-white p-3 rounded-[1.5rem] shadow-2xl border border-slate-200 flex items-center gap-4 group">
             <div className="text-[10px] font-black text-slate-400 uppercase tracking-[0.2em] ml-4">Filter Agenda:</div>
             <select className="border-none bg-slate-50 rounded-2xl px-6 py-4 text-sm font-black text-slate-800 outline-none cursor-pointer min-w-[280px] appearance-none" value={selectedTripId || ''} onChange={(e) => setSelectedTripId(Number(e.target.value))}>
               {trips.map(t => <option key={t.id} value={t.id}>{t.title}</option>)}
             </select>
          </div>
        </div>

        {activeModule === 'summary' && (
          <div className="space-y-10 animate-in fade-in duration-700">
            <div className="grid grid-cols-1 md:grid-cols-2 gap-8">
              <Card className="p-10 border-none shadow-2xl bg-gradient-to-br from-emerald-600 to-emerald-800 text-white relative group overflow-hidden">
                <div className="absolute top-0 right-0 w-32 h-32 bg-white/10 rounded-full -mr-16 -mt-16 group-hover:scale-150 transition duration-700"></div>
                <div className="text-[11px] font-black uppercase tracking-[0.4em] opacity-60 mb-2">Omzet Bersih</div>
                <div className="text-5xl font-black tracking-tighter italic">{formatRupiah(stats.revenue)}</div>
              </Card>
              <Card className="p-10 border-none shadow-2xl bg-gradient-to-br from-blue-600 to-blue-800 text-white relative group overflow-hidden">
                <div className="absolute top-0 right-0 w-32 h-32 bg-white/10 rounded-full -mr-16 -mt-16 group-hover:scale-150 transition duration-700"></div>
                <div className="text-[11px] font-black uppercase tracking-[0.4em] opacity-60 mb-2">Laba Trip</div>
                <div className="text-5xl font-black tracking-tighter italic">{formatRupiah(stats.profit)}</div>
              </Card>
            </div>
            <Card className="p-12 rounded-[2.5rem] border-none shadow-2xl">
              <h3 className="font-black text-2xl text-slate-800 mb-10 flex items-center gap-5 uppercase tracking-tighter italic border-b-2 border-slate-50 pb-6"><Calculator className="text-emerald-600" size={32}/> Laporan Keuangan</h3>
              <SimpleBarChart label="Total Pendapatan" value={stats.revenue} total={stats.revenue} colorClass="bg-emerald-500 shadow-xl shadow-emerald-100" />
              <div className="my-10"></div>
              <SimpleBarChart label="Total Pengeluaran" value={stats.expenses} total={stats.revenue} colorClass="bg-red-500 shadow-xl shadow-red-100" />
            </Card>
          </div>
        )}

        {activeModule === 'trips' && (
          <div className="space-y-8 animate-in slide-in-from-bottom-8">
            <div className="flex justify-end">
              <button onClick={() => openTripModal('add')} className="bg-emerald-600 text-white px-10 py-5 rounded-[1.5rem] font-black text-xs uppercase tracking-widest flex items-center gap-4 hover:bg-emerald-700 shadow-2xl active:scale-95"><Plus size={20} /> Agenda Baru</button>
            </div>
            <div className="grid gap-6">
              {trips.map(t => (
                <Card key={t.id} className="p-8 flex justify-between items-center group hover:border-emerald-400 transition-all rounded-[2rem] border-2 shadow-lg">
                  <div className="flex items-center gap-8">
                    <div className={`w-16 h-16 rounded-2xl flex items-center justify-center shadow-inner ${t.status === 'open' ? 'bg-emerald-50 text-emerald-600' : 'bg-slate-50 text-slate-400'}`}><Plane size={32}/></div>
                    <div>
                      <div className="font-black text-slate-900 text-2xl uppercase italic tracking-tighter">{t.title}</div>
                      <div className="text-xs text-slate-400 font-black flex gap-8 mt-2 uppercase tracking-[0.1em] opacity-80">
                        <span className="flex items-center gap-2"><MapPin size={16}/> {t.city}</span>
                        <span className="flex items-center gap-2"><Calendar size={16}/> {formatDate(t.date_start)}</span>
                      </div>
                    </div>
                  </div>
                  <div className="flex items-center gap-3">
                    <button onClick={() => openTripModal('edit', t)} className="p-3 text-slate-400 hover:text-emerald-600 hover:bg-emerald-50 rounded-2xl transition border-2 border-transparent hover:border-emerald-100"><Edit size={24}/></button>
                    <button onClick={() => confirmDelete('trips', t.id, t.title)} className="p-3 text-slate-400 hover:text-red-600 hover:bg-red-50 rounded-2xl transition border-2 border-transparent hover:border-red-100"><Trash2 size={24}/></button>
                  </div>
                </Card>
              ))}
            </div>
          </div>
        )}

        {activeModule === 'products' && (
          <div className="space-y-8 animate-in slide-in-from-bottom-8">
            <div className="flex justify-between items-center bg-white p-10 rounded-[2.5rem] shadow-2xl border border-slate-100">
              <div>
                <h3 className="font-black text-slate-900 uppercase tracking-tighter text-2xl italic">Kontrol Katalog</h3>
                <div className="text-[10px] text-slate-400 font-black mt-1 uppercase tracking-widest italic italic">Agenda: <b className="text-emerald-600">{activeTrip?.title || '-'}</b></div>
              </div>
              <button onClick={() => openProdModal('add')} className="bg-emerald-600 text-white px-10 py-5 rounded-[1.5rem] font-black text-xs uppercase tracking-widest flex items-center gap-4 hover:bg-emerald-700 shadow-2xl active:scale-95"><Plus size={20} /> Tambah Item</button>
            </div>
            <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-2 xl:grid-cols-3 gap-10">
              {filteredProducts.map(p => {
                const total = Number(p.price_buy) + (Number(p.fee) || 0);
                return (
                <Card key={p.id} className="flex p-8 gap-8 items-center group hover:border-emerald-400 transition-all duration-500 rounded-[2.5rem] border-2 shadow-xl min-h-[220px]">
                  <div className="w-28 h-28 bg-slate-100 rounded-[2rem] overflow-hidden flex-shrink-0 shadow-2xl relative">
                    <img src={p.image} className="w-full h-full object-cover group-hover:scale-110 transition duration-500" onError={(e) => e.target.src='https://placehold.co/400x400?text=Produk'} />
                  </div>
                  <div className="flex-1 min-w-0">
                    <div className="font-black text-slate-900 truncate text-xl uppercase tracking-tighter mb-4">{p.name}</div>
                    <div className="grid grid-cols-2 gap-y-2 text-[11px] font-black border-t-2 pt-4 border-slate-50 uppercase tracking-tight italic">
                      <div className="text-slate-400">Beli:</div>
                      <div className="text-slate-700 text-right">{formatRupiah(p.price_buy)}</div>
                      <div className="text-slate-400">Fee:</div>
                      <div className="text-orange-600 text-right">+{formatRupiah(p.fee)}</div>
                      <div className="text-slate-900 font-black pt-2 border-t mt-2">TOTAL:</div>
                      <div className="font-black text-emerald-700 text-lg text-right pt-1 border-t mt-2 tracking-tighter italic">{formatRupiah(total)}</div>
                    </div>
                  </div>
                  <div className="flex flex-col gap-3 flex-shrink-0">
                    <button onClick={() => openProdModal('edit', p)} className="p-3 text-slate-400 hover:text-blue-600 transition hover:bg-blue-50 rounded-2xl border-2 border-slate-50 shadow-sm"><Edit size={22}/></button>
                    <button onClick={() => confirmDelete('products', p.id, p.name)} className="p-3 text-slate-400 hover:text-red-600 transition hover:bg-red-50 rounded-2xl border-2 border-slate-50 shadow-sm"><Trash2 size={22}/></button>
                  </div>
                </Card>
              )})}
            </div>
          </div>
        )}

        {activeModule === 'finance' && (
          <div className="grid grid-cols-1 lg:grid-cols-2 gap-14 animate-in slide-in-from-bottom-8">
            <div className="space-y-10">
              <div className="flex justify-between items-center bg-emerald-50 p-8 rounded-[2.5rem] border-2 border-emerald-100 shadow-xl italic italic">
                <h3 className="font-black text-emerald-800 uppercase tracking-widest flex items-center gap-4 text-sm"><TrendingUp size={32}/> Pesanan Masuk</h3>
                <button onClick={() => openFinModal('order', 'add')} className="bg-emerald-600 text-white p-4 rounded-[1.2rem] shadow-2xl hover:bg-emerald-700 active:scale-90 shadow-xl"><Plus size={28}/></button>
              </div>
              <div className="space-y-5">
                {filteredOrders.map(o => (
                  <Card key={o.id} className="p-10 flex justify-between items-center border-l-[12px] border-l-emerald-500 shadow-2xl rounded-[2.5rem] border-2 group hover:border-emerald-300 transition">
                    <div><div className="font-black text-slate-900 text-2xl uppercase tracking-tighter italic">{o.customer_name}</div><div className="text-[10px] text-slate-400 font-black mt-1 uppercase tracking-widest italic opacity-70 italic">{formatDate(o.created_at)}</div></div>
                    <div className="flex items-center gap-6 flex-shrink-0">
                      <div className="font-black text-emerald-600 text-3xl tracking-tighter italic">{formatRupiah(o.total)}</div>
                      <div className="flex gap-2">
                        <button onClick={() => openFinModal('order', 'edit', o)} className="text-slate-400 hover:text-blue-500 p-2 border border-slate-100 rounded-lg"><Edit size={22}/></button>
                        <button onClick={() => confirmDelete('orders', o.id, `Pesanan ${o.customer_name}`)} className="text-slate-300 hover:text-red-500 p-2 border border-slate-100 rounded-lg"><Trash2 size={22}/></button>
                      </div>
                    </div>
                  </Card>
                ))}
              </div>
            </div>

            <div className="space-y-10">
              <div className="flex justify-between items-center bg-red-50 p-8 rounded-[2.5rem] border-2 border-red-100 shadow-xl italic italic">
                <h3 className="font-black text-red-800 uppercase tracking-widest flex items-center gap-4 text-sm"><TrendingDown size={32}/> Biaya Operasional</h3>
                <button onClick={() => openFinModal('expense', 'add')} className="bg-red-600 text-white p-4 rounded-[1.2rem] shadow-2xl hover:bg-red-700 active:scale-90 shadow-xl"><Plus size={28}/></button>
              </div>
              <div className="space-y-5">
                {filteredExpenses.map(e => (
                  <Card key={e.id} className="p-10 flex justify-between items-center border-l-[12px] border-l-red-500 shadow-2xl rounded-[2.5rem] border-2 group hover:border-red-300 transition">
                    <div className="flex-1 min-w-0 pr-10 italic"><div className="font-black text-slate-900 truncate uppercase text-2xl tracking-tighter italic">{e.description}</div><div className="text-[10px] text-red-400 font-black mt-1 uppercase tracking-widest italic opacity-70 italic italic italic">{e.category}</div></div>
                    <div className="flex items-center gap-6 flex-shrink-0">
                      <div className="font-black text-red-600 text-3xl tracking-tighter italic">({formatRupiah(e.amount)})</div>
                      <div className="flex gap-2">
                        <button onClick={() => openFinModal('expense', 'edit', e)} className="text-slate-400 hover:text-blue-500 p-2 border border-slate-100 rounded-lg"><Edit size={22}/></button>
                        <button onClick={() => confirmDelete('expenses', e.id, e.description)} className="text-slate-300 hover:text-red-500 p-2 border border-slate-100 rounded-lg"><Trash2 size={22}/></button>
                      </div>
                    </div>
                  </Card>
                ))}
              </div>
            </div>
          </div>
        )}
      </main>

      {/* --- ALL MODALS --- */}
      
      {deleteConfirm.open && (
        <div className="fixed inset-0 bg-black/95 z-[200] flex items-center justify-center p-6 backdrop-blur-xl animate-in fade-in zoom-in duration-300">
          <Card className="w-full max-w-sm p-12 shadow-2xl border-none rounded-[3rem]">
            <div className="text-center">
              <div className="bg-red-100 w-24 h-24 rounded-[2rem] flex items-center justify-center mx-auto mb-10 shadow-2xl shadow-red-500/20"><Trash2 className="text-red-600" size={48} /></div>
              <h3 className="font-black text-3xl text-slate-900 mb-4 uppercase tracking-tighter italic italic italic">Hapus Data?</h3>
              <p className="text-slate-500 text-sm font-bold leading-relaxed opacity-80 uppercase tracking-widest text-center">Yakin ingin membuang <br/><b className="text-slate-900 font-black text-base tracking-normal">"{deleteConfirm.label}"</b>?</p>
              <div className="grid grid-cols-2 gap-6 mt-12">
                <button onClick={() => setDeleteConfirm({ ...deleteConfirm, open: false })} className="bg-slate-100 text-slate-500 py-5 rounded-2xl font-black text-xs uppercase tracking-[0.3em] active:scale-95">Batal</button>
                <button onClick={processDelete} disabled={isSaving} className="bg-red-600 text-white py-5 rounded-2xl font-black text-xs uppercase tracking-[0.3em] shadow-2xl active:scale-95 transition flex justify-center items-center gap-2">{isSaving ? <Loader2 className="animate-spin" size={14}/> : 'Hapus'}</button>
              </div>
            </div>
          </Card>
        </div>
      )}

      {financeModal.open && (
        <div className="fixed inset-0 bg-black/80 z-[100] flex items-center justify-center p-4 backdrop-blur-md animate-in fade-in duration-300 overflow-y-auto">
          <Card className="w-full max-w-md p-10 md:p-12 shadow-2xl border-none rounded-[3rem] my-auto max-h-[90vh] overflow-y-auto">
            <h3 className="font-black text-3xl text-slate-900 uppercase tracking-tighter italic mb-8 border-b-2 border-slate-50 pb-6">
              {financeModal.mode === 'edit' ? 'Update' : 'Entry'} {financeModal.type === 'order' ? 'Pemasukan' : 'Biaya'}
            </h3>
            <form onSubmit={handleSaveFinance} className="space-y-6">
              {financeModal.type === 'order' ? (
                <>
                  <div className="space-y-1">
                    <label className="text-[10px] font-black text-slate-400 uppercase tracking-widest ml-1 opacity-70">Nama Pelanggan</label>
                    <input className="w-full border-slate-200 border-2 p-3.5 rounded-2xl font-black outline-none focus:ring-4 focus:ring-emerald-100 transition shadow-inner uppercase" placeholder="NAMA..." required value={finForm.customer_name} onChange={e => setFinForm({...finForm, customer_name: e.target.value})} />
                  </div>
                  <div className="space-y-1">
                    <label className="text-[10px] font-black text-slate-400 uppercase tracking-widest ml-1 opacity-70">Total Bayar (Rp)</label>
                    <input className="w-full border-slate-200 border-2 p-3.5 rounded-2xl font-black outline-none focus:ring-4 focus:ring-emerald-100 transition text-emerald-700 text-2xl shadow-inner tracking-tighter" type="number" placeholder="0" required value={finForm.total} onChange={e => setFinForm({...finForm, total: e.target.value})} />
                  </div>
                </>
              ) : (
                <>
                  <div className="space-y-1">
                    <label className="text-[10px] font-black text-slate-400 uppercase tracking-widest ml-1 opacity-70">Kategori Biaya</label>
                    <div className="flex items-center gap-3 bg-slate-50 p-1.5 rounded-2xl border border-slate-100 italic italic">
                      <Tag className="text-slate-400 ml-3" size={18}/>
                      <select className="flex-1 bg-transparent border-none p-2 font-black outline-none uppercase text-xs text-slate-700" value={finForm.category} onChange={e => setFinForm({...finForm, category: e.target.value})}>
                        <option value="Transport">Transport (Bensin/Grab/Tol)</option>
                        <option value="Akomodasi">Akomodasi (Hotel/Parkir)</option>
                        <option value="Konsumsi">Konsumsi (Makan Team)</option>
                        <option value="Lainnya">Pengeluaran Lainnya</option>
                      </select>
                    </div>
                  </div>
                  <div className="space-y-1">
                    <label className="text-[10px] font-black text-slate-400 uppercase tracking-widest ml-1 opacity-70">Keterangan Detail</label>
                    <div className="flex items-center gap-3 bg-slate-50 p-1.5 rounded-2xl border border-slate-100 italic italic">
                      <FileText className="text-slate-400 ml-3" size={18}/>
                      <input className="flex-1 bg-transparent border-none p-2 font-black outline-none uppercase text-sm text-slate-700" placeholder="DESKRIPSI..." required value={finForm.description} onChange={e => setFinForm({...finForm, description: e.target.value})} />
                    </div>
                  </div>
                  <div className="space-y-1">
                    <label className="text-[10px] font-black text-slate-400 uppercase tracking-widest ml-1 opacity-70">Nominal (Rp)</label>
                    <input className="w-full border-slate-200 border-2 p-3.5 rounded-2xl font-black outline-none focus:ring-4 focus:ring-red-100 text-red-700 text-2xl shadow-inner tracking-tighter italic" type="number" placeholder="0" required value={finForm.amount} onChange={e => setFinForm({...finForm, amount: e.target.value})} />
                  </div>
                </>
              )}
              <div className="flex gap-4 pt-4">
                <button type="button" onClick={() => setFinanceModal({ ...financeModal, open: false })} className="flex-1 bg-slate-100 text-slate-500 py-5 rounded-2xl font-black text-[10px] uppercase tracking-widest active:scale-95 italic italic italic">Batal</button>
                <button disabled={isSaving} className={`flex-1 text-white py-5 rounded-2xl font-black text-[10px] uppercase tracking-widest shadow-2xl flex justify-center items-center gap-3 active:scale-95 transition ${financeModal.type === 'order' ? 'bg-emerald-600 hover:bg-emerald-700' : 'bg-red-600 hover:bg-red-700'}`}>
                  {isSaving ? <Loader2 className="animate-spin" size={20}/> : <Save size={20}/>} Simpan Cloud
                </button>
              </div>
            </form>
          </Card>
        </div>
      )}

      {productModal.open && (
        <div className="fixed inset-0 bg-black/80 z-[100] flex items-center justify-center p-4 backdrop-blur-md animate-in fade-in duration-300">
          <Card className="w-full max-w-lg p-10 md:p-12 shadow-2xl border-none rounded-[3rem] my-auto max-h-[90vh] overflow-y-auto italic">
            <h3 className="font-black text-3xl text-slate-900 uppercase tracking-tighter italic mb-8 border-b-2 border-slate-50 pb-6 flex items-center gap-5">
              <ShoppingBag className="text-emerald-600" size={40}/> {productModal.type === 'add' ? 'Katalog Baru' : 'Update Item'}
            </h3>
            <form onSubmit={handleSaveProduct} className="space-y-6">
              <div className="space-y-1">
                <label className="text-[10px] font-black text-slate-400 uppercase tracking-widest ml-1 opacity-70 italic italic">Nama Barang</label>
                <input className="w-full border-slate-200 border-2 p-3.5 rounded-2xl font-black outline-none focus:ring-4 focus:ring-emerald-100 shadow-inner uppercase italic" placeholder="SPIKOE RAISIN..." required value={prodForm.name} onChange={e => setProdForm({...prodForm, name: e.target.value})} />
              </div>
              <div className="space-y-1">
                <label className="text-[10px] font-black text-slate-400 uppercase tracking-widest ml-1 opacity-70 italic italic">Deskripsi Singkat</label>
                <textarea className="w-full border-slate-200 border-2 p-3.5 rounded-2xl font-black outline-none focus:ring-4 focus:ring-emerald-100 shadow-inner uppercase text-sm italic" placeholder="DETAIL PRODUK..." rows="2" value={prodForm.description} onChange={e => setProdForm({...prodForm, description: e.target.value})} />
              </div>
              <div className="grid grid-cols-2 gap-5 italic italic">
                <div className="space-y-1">
                  <label className="text-[10px] font-black text-slate-400 uppercase tracking-widest ml-1 opacity-70 italic">Harga Beli</label>
                  <input className="w-full border-slate-200 border-2 p-3.5 rounded-2xl font-black outline-none focus:ring-4 focus:ring-emerald-100 shadow-inner italic" type="number" placeholder="0" required value={prodForm.price_buy} onChange={e => setProdForm({...prodForm, price_buy: e.target.value})} />
                </div>
                <div className="space-y-1">
                  <label className="text-[10px] font-black text-orange-600 uppercase tracking-widest ml-1 opacity-70 italic">Laba Jastip</label>
                  <input className="w-full border-orange-200 border-2 p-3.5 rounded-2xl font-black outline-none focus:ring-4 focus:ring-orange-100 bg-orange-50 text-orange-900 shadow-inner italic" type="number" placeholder="0" required value={prodForm.fee} onChange={e => setProdForm({...prodForm, fee: e.target.value})} />
                </div>
              </div>
              <div className="bg-emerald-50 p-5 rounded-[2rem] flex items-center gap-6 text-emerald-800 border-2 border-emerald-100 shadow-inner font-black italic">
                <Calculator size={36} className="opacity-40" />
                <div className="flex-1 italic italic">
                  <div className="text-[9px] uppercase tracking-widest opacity-60 mb-1">Harga Jual Otomatis:</div>
                  <div className="text-3xl font-black tracking-tighter leading-none">{formatRupiah((parseInt(prodForm.price_buy)||0) + (parseInt(prodForm.fee)||0))}</div>
                </div>
              </div>
              <div className="space-y-1">
                <label className="text-[10px] font-black text-slate-400 uppercase tracking-widest ml-1 opacity-70">Link Gambar Supabase</label>
                <input className="w-full border-slate-200 border-2 p-3.5 rounded-2xl font-black text-xs text-slate-500 shadow-inner italic" placeholder="URL..." value={prodForm.image_url} onChange={e => setProdForm({...prodForm, image_url: e.target.value})} />
              </div>
              <div className="pt-4 italic italic">
                <button disabled={isSaving} className="w-full bg-emerald-600 text-white py-4 rounded-2xl font-black text-xs uppercase tracking-widest shadow-2xl flex justify-center items-center gap-3 active:scale-95 transition italic">
                  {isSaving ? <Loader2 className="animate-spin" size={20}/> : <CheckCircle2 size={20}/>} Simpan Data Cloud
                </button>
              </div>
            </form>
          </Card>
        </div>
      )}

      {tripModal.open && (
        <div className="fixed inset-0 bg-black/80 z-[100] flex items-center justify-center p-4 backdrop-blur-md animate-in fade-in duration-300">
          <Card className="w-full max-w-lg p-10 md:p-12 shadow-2xl border-none rounded-[3rem] my-auto max-h-[90vh] overflow-y-auto italic">
            <h3 className="font-black text-3xl text-slate-900 uppercase tracking-tighter italic mb-8 flex items-center gap-5 italic italic">
              <Plane className="text-emerald-600" size={40}/> Agenda Trip
            </h3>
            <form onSubmit={handleSaveTrip} className="space-y-6 italic italic italic">
              <div className="space-y-1">
                <label className="text-[10px] font-black text-slate-400 uppercase tracking-widest ml-1 opacity-70">Judul Agenda</label>
                <input className="w-full border-slate-200 border-2 p-3.5 rounded-2xl font-black outline-none focus:ring-4 focus:ring-emerald-100 shadow-inner uppercase text-sm italic italic" placeholder="SPIKOE BATCH 2..." required value={tripForm.title} onChange={e => setTripForm({...tripForm, title: e.target.value})} />
              </div>
              <div className="space-y-1">
                <label className="text-[10px] font-black text-slate-400 uppercase tracking-widest ml-1 opacity-70">Kota Tujuan</label>
                <input className="w-full border-slate-200 border-2 p-3.5 rounded-2xl font-black outline-none focus:ring-4 focus:ring-emerald-100 shadow-inner uppercase text-sm italic italic" placeholder="SURABAYA..." required value={tripForm.city} onChange={e => setTripForm({...tripForm, city: e.target.value})} />
              </div>
              <div className="grid grid-cols-2 gap-6 italic italic">
                <div>
                  <label className="text-[10px] font-black text-slate-400 uppercase tracking-widest ml-1 mb-2 block italic">Tgl Berangkat</label>
                  <input type="date" className="w-full border-slate-200 border-2 p-3.5 rounded-2xl font-black outline-none shadow-inner italic" value={tripForm.date_start} onChange={e => setTripForm({...tripForm, date_start: e.target.value})} />
                </div>
                <div>
                  <label className="text-[10px] font-black text-orange-600 uppercase tracking-widest ml-1 mb-2 block italic opacity-80 italic">Close PO</label>
                  <input type="date" className="w-full border-orange-200 border-2 p-3.5 rounded-2xl font-black bg-orange-50 text-orange-900 shadow-inner focus:ring-4 focus:ring-orange-100 outline-none italic" value={tripForm.deadline} onChange={e => setTripForm({...tripForm, deadline: e.target.value})} />
                </div>
              </div>
              <div className="pt-8 flex gap-6 italic italic italic">
                <button type="button" onClick={() => setTripModal({ ...tripModal, open: false })} className="flex-1 bg-slate-100 text-slate-500 py-5 rounded-2xl font-black text-[10px] uppercase tracking-widest active:scale-95 italic">Batal</button>
                <button disabled={isSaving} className="flex-1 bg-emerald-600 text-white py-4 rounded-2xl font-black text-[10px] uppercase tracking-widest shadow-2xl flex justify-center items-center gap-3 active:scale-95 transition shadow-xl italic">
                  {isSaving ? <Loader2 className="animate-spin" size={20}/> : <Save size={20}/>} Simpan Agenda
                </button>
              </div>
            </form>
          </Card>
        </div>
      )}
    </div>
  );
}