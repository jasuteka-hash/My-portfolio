# My-portfolio
自己紹介用のポートフォリオサイト
import React, { useState, useEffect } from 'react';
import { Menu, X, ArrowRight, MapPin, Clock, ShoppingBag, Instagram, ChevronRight } from 'lucide-react';

// --- Components ---

const Navbar = () => {
  const [isScrolled, setIsScrolled] = useState(false);
  const [isMenuOpen, setIsMenuOpen] = useState(false);

  useEffect(() => {
    const handleScroll = () => setIsScrolled(window.scrollY > 50);
    window.addEventListener('scroll', handleScroll);
    return () => window.removeEventListener('scroll', handleScroll);
  }, []);

  const navLinks = [
    { name: 'Philosophy', href: '#philosophy' },
    { name: 'Tea & Menu', href: '#menu' },
    { name: 'Space', href: '#space' },
    { name: 'Shop', href: '#shop' },
  ];

  return (
    <nav className={`fixed w-full z-50 transition-all duration-500 ${isScrolled ? 'bg-white/90 backdrop-blur-md py-4 shadow-sm' : 'bg-transparent py-8'}`}>
      <div className="max-w-7xl mx-auto px-6 flex justify-between items-center">
        <div className={`text-2xl font-serif tracking-widest transition-colors duration-300 ${isScrolled ? 'text-zinc-900' : 'text-white'}`}>
          茶寮 翠葉
        </div>
        
        {/* Desktop Links */}
        <div className="hidden md:flex items-center space-x-10">
          {navLinks.map((link) => (
            <a 
              key={link.name} 
              href={link.href} 
              className={`text-sm tracking-widest hover:opacity-60 transition-opacity ${isScrolled ? 'text-zinc-800' : 'text-white'}`}
            >
              {link.name}
            </a>
          ))}
          <button className="bg-emerald-900 text-white px-8 py-3 text-sm tracking-widest hover:bg-emerald-800 transition-colors">
            ご予約
          </button>
        </div>

        {/* Mobile Toggle */}
        <button className="md:hidden" onClick={() => setIsMenuOpen(!isMenuOpen)}>
          {isMenuOpen ? <X className="text-zinc-900" /> : <Menu className={isScrolled ? 'text-zinc-900' : 'text-white'} />}
        </button>
      </div>

      {/* Mobile Menu Overlay */}
      {isMenuOpen && (
        <div className="fixed inset-0 bg-white z-50 flex flex-col items-center justify-center space-y-8 animate-in fade-in zoom-in duration-300">
          <button className="absolute top-8 right-6" onClick={() => setIsMenuOpen(false)}>
            <X size={32} />
          </button>
          {navLinks.map((link) => (
            <a key={link.name} href={link.href} onClick={() => setIsMenuOpen(false)} className="text-2xl font-serif tracking-widest">
              {link.name}
            </a>
          ))}
          <button className="bg-emerald-900 text-white px-12 py-4 text-lg tracking-widest">
            ご予約
          </button>
        </div>
      )}
    </nav>
  );
};

const SectionHeading = ({ subtitle, title, light = false }) => (
  <div className="mb-16 text-center">
    <p className={`text-xs tracking-[0.3em] uppercase mb-4 ${light ? 'text-emerald-200' : 'text-emerald-800 font-bold'}`}>
      {subtitle}
    </p>
    <h2 className={`text-3xl md:text-4xl font-serif leading-relaxed ${light ? 'text-white' : 'text-zinc-800'}`}>
      {title}
    </h2>
  </div>
);

const App = () => {
  return (
    <div className="min-h-screen bg-[#fdfcf8] text-zinc-800 selection:bg-emerald-100 selection:text-emerald-900 font-sans">
      <Navbar />

      {/* Hero Section */}
      <section className="relative h-screen flex items-center justify-center overflow-hidden">
        <div className="absolute inset-0 bg-black/40 z-10" />
        <div 
          className="absolute inset-0 bg-cover bg-center transition-transform duration-[10s] scale-110 hover:scale-100"
          style={{ backgroundImage: 'url("https://images.unsplash.com/photo-1544967082-d9d25d867d66?auto=format&fit=crop&q=80&w=2000")' }}
        />
        <div className="relative z-20 text-center text-white px-4">
          <p className="text-sm tracking-[0.5em] mb-6 animate-pulse">EST. 1892 / KYOTO</p>
          <h1 className="text-5xl md:text-7xl lg:text-8xl font-serif mb-12 leading-tight tracking-wider">
            一服の茶に、<br />
            心を澄ます。
          </h1>
          <div className="flex flex-col md:flex-row items-center justify-center gap-6">
            <button className="group flex items-center gap-3 border border-white/40 bg-white/10 backdrop-blur-sm px-10 py-4 hover:bg-white hover:text-zinc-900 transition-all duration-500">
              <span className="tracking-[0.2em] text-sm font-medium">VIEW MENU</span>
              <ArrowRight size={18} className="group-hover:translate-x-2 transition-transform" />
            </button>
          </div>
        </div>
        <div className="absolute bottom-10 left-1/2 -translate-x-1/2 z-20 hidden md:block">
          <div className="w-px h-24 bg-gradient-to-b from-white to-transparent" />
        </div>
      </section>

      {/* Philosophy Section */}
      <section id="philosophy" className="py-32 px-6">
        <div className="max-w-5xl mx-auto">
          <div className="grid md:grid-cols-2 gap-20 items-center">
            <div className="relative">
              <div className="aspect-[4/5] overflow-hidden">
                <img 
                  src="https://images.unsplash.com/photo-1563450212267-02484439798a?auto=format&fit=crop&q=80&w=1000" 
                  alt="Tea preparation" 
                  className="w-full h-full object-cover hover:scale-105 transition-transform duration-700"
                />
              </div>
              <div className="absolute -bottom-10 -right-10 hidden md:block w-64 h-80 overflow-hidden shadow-2xl border-4 border-[#fdfcf8]">
                <img 
                  src="https://images.unsplash.com/photo-1576092768241-dec231879fc3?auto=format&fit=crop&q=80&w=600" 
                  alt="Detail" 
                  className="w-full h-full object-cover hover:scale-105 transition-transform duration-700"
                />
              </div>
            </div>
            <div className="space-y-8">
              <SectionHeading subtitle="Philosophy" title="伝統と革新の調和" />
              <p className="leading-loose text-zinc-600">
                明治二十五年、京都の地で創業した翠葉。私たちが守り続けてきたのは、茶葉一葉に込められた自然の恵みと、それを受け止める人の心です。<br /><br />
                時代が移ろい、生活の様式が変わっても、一杯の茶がもたらす「静寂」の価値は変わりません。伝統的な茶の湯の精神を大切にしながら、現代の日常に馴染む、新しいお茶の愉しみ方を提案します。
              </p>
              <a href="#" className="inline-flex items-center gap-2 text-emerald-900 font-bold tracking-widest text-sm group">
                READ OUR STORY 
                <ChevronRight size={16} className="group-hover:translate-x-1 transition-transform" />
              </a>
            </div>
          </div>
        </div>
      </section>

      {/* Menu Highlight Section */}
      <section id="menu" className="py-32 bg-zinc-900 text-white">
        <div className="max-w-7xl mx-auto px-6">
          <SectionHeading subtitle="Seasonal Collection" title="旬を味わう、翠葉のお品書き" light />
          
          <div className="grid md:grid-cols-3 gap-12">
            {[
              { 
                name: '極み抹茶「千代の昔」', 
                desc: '石臼で丁寧に挽きあげた、芳醇な香りと甘みが特徴の最高級抹茶。',
                price: '¥1,800',
                img: 'https://images.unsplash.com/photo-1515696955266-4f67e13219e8?auto=format&fit=crop&q=80&w=800'
              },
              { 
                name: '季節の主菓子セット', 
                desc: '二十四節気に合わせた職人手作りの生菓子と、お好みの日本茶を。',
                price: '¥2,400',
                img: 'https://images.unsplash.com/photo-1582722427702-8373ee9f925b?auto=format&fit=crop&q=80&w=800'
              },
              { 
                name: '抹茶アフォガート', 
                desc: '濃厚なバニラアイスに、その場で点てた濃茶をかけて。',
                price: '¥1,500',
                img: 'https://images.unsplash.com/photo-1506368249639-73a05d6f6488?auto=format&fit=crop&q=80&w=800'
              }
            ].map((item, i) => (
              <div key={i} className="group cursor-pointer">
                <div className="aspect-square overflow-hidden mb-6 relative">
                  <img 
                    src={item.img} 
                    alt={item.name} 
                    className="w-full h-full object-cover transition-transform duration-700 group-hover:scale-110 opacity-80 group-hover:opacity-100"
                  />
                  <div className="absolute bottom-4 right-4 bg-white/10 backdrop-blur-md px-4 py-2 text-xs">
                    {item.price}
                  </div>
                </div>
                <h3 className="text-xl font-serif mb-3 tracking-wide">{item.name}</h3>
                <p className="text-sm text-zinc-400 leading-relaxed mb-4">{item.desc}</p>
              </div>
            ))}
          </div>
        </div>
      </section>

      {/* Location / Reservation CTA */}
      <section id="space" className="py-32 px-6">
        <div className="max-w-4xl mx-auto text-center border border-zinc-200 p-12 md:p-24 relative bg-white shadow-sm overflow-hidden">
          <div className="absolute top-0 left-0 w-2 h-full bg-emerald-900" />
          <SectionHeading subtitle="Experience" title="至福のひとときを、ご予約で" />
          <p className="text-zinc-600 mb-12 max-w-2xl mx-auto leading-loose">
            都会の喧騒を離れ、静謐な空間で、点てたてのお茶をお愉しみいただけます。<br />
            茶席のご予約は二ヶ月前より承っております。
          </p>
          
          <div className="grid md:grid-cols-2 gap-8 mb-12 text-left max-w-xl mx-auto">
            <div className="flex items-start gap-4">
              <Clock className="text-emerald-900 shrink-0" size={20} />
              <div>
                <h4 className="font-bold text-sm mb-1">営業時間</h4>
                <p className="text-sm text-zinc-500">11:00 — 18:00 (L.O. 17:30)</p>
                <p className="text-sm text-zinc-500 italic">定休日：火曜日</p>
              </div>
            </div>
            <div className="flex items-start gap-4">
              <MapPin className="text-emerald-900 shrink-0" size={20} />
              <div>
                <h4 className="font-bold text-sm mb-1">所在地</h4>
                <p className="text-sm text-zinc-500">京都府京都市東山区祇園町...</p>
                <p className="text-sm text-zinc-500 underline cursor-pointer hover:text-emerald-800">Google Mapsで見る</p>
              </div>
            </div>
          </div>

          <button className="bg-emerald-900 text-white px-16 py-5 tracking-[0.2em] font-medium hover:bg-emerald-800 transition-all transform hover:-translate-y-1 shadow-lg shadow-emerald-900/20">
            茶席の空き状況を確認する
          </button>
        </div>
      </section>

      {/* Online Shop Banner */}
      <section id="shop" className="py-20 bg-emerald-900 text-white overflow-hidden relative">
        <div className="max-w-7xl mx-auto px-6 relative z-10">
          <div className="flex flex-col md:flex-row items-center justify-between gap-10">
            <div>
              <h2 className="text-3xl md:text-4xl font-serif mb-4">翠葉の味を、ご自宅で。</h2>
              <p className="text-emerald-100/80 mb-0">厳選した茶葉、茶菓子をオンラインストアでお求めいただけます。</p>
            </div>
            <button className="flex items-center gap-3 bg-white text-emerald-900 px-10 py-4 font-bold tracking-widest hover:bg-zinc-100 transition-colors">
              <ShoppingBag size={20} />
              ONLINE STORE
            </button>
          </div>
        </div>
        <div className="absolute top-0 right-0 opacity-10 -translate-y-1/2 translate-x-1/2 scale-150 pointer-events-none">
           {/* Decorative SVG pattern */}
           <svg width="400" height="400" viewBox="0 0 100 100">
             <circle cx="50" cy="50" r="45" fill="none" stroke="white" strokeWidth="0.5" />
             <path d="M50 5 L50 95 M5 50 L95 50" stroke="white" strokeWidth="0.5" />
           </svg>
        </div>
      </section>

      {/* Footer */}
      <footer className="bg-white py-20 px-6 border-t border-zinc-100">
        <div className="max-w-7xl mx-auto">
          <div className="grid md:grid-cols-4 gap-12 mb-20">
            <div className="col-span-2">
              <div className="text-2xl font-serif tracking-widest mb-8">茶寮 翠葉</div>
              <p className="text-sm text-zinc-500 leading-relaxed max-w-sm mb-8">
                一杯のお茶を通じて、日々の暮らしに余白を。<br />
                私たちは茶文化の継承と、新しい価値の創造に努めています。
              </p>
              <div className="flex gap-4">
                <div className="w-10 h-10 border border-zinc-200 rounded-full flex items-center justify-center hover:bg-zinc-50 transition-colors cursor-pointer text-zinc-600">
                  <Instagram size={18} />
                </div>
              </div>
            </div>
            <div>
              <h4 className="font-bold text-xs tracking-[0.2em] uppercase mb-6">Explore</h4>
              <ul className="space-y-4 text-sm text-zinc-500">
                <li><a href="#" className="hover:text-emerald-900 transition-colors">Philosophy</a></li>
                <li><a href="#" className="hover:text-emerald-900 transition-colors">Sitemap</a></li>
                <li><a href="#" className="hover:text-emerald-900 transition-colors">Press</a></li>
                <li><a href="#" className="hover:text-emerald-900 transition-colors">Recruit</a></li>
              </ul>
            </div>
            <div>
              <h4 className="font-bold text-xs tracking-[0.2em] uppercase mb-6">Support</h4>
              <ul className="space-y-4 text-sm text-zinc-500">
                <li><a href="#" className="hover:text-emerald-900 transition-colors">Contact</a></li>
                <li><a href="#" className="hover:text-emerald-900 transition-colors">FAQ</a></li>
                <li><a href="#" className="hover:text-emerald-900 transition-colors">Privacy Policy</a></li>
                <li><a href="#" className="hover:text-emerald-900 transition-colors">Official Blog</a></li>
              </ul>
            </div>
          </div>
          <div className="text-[10px] text-zinc-400 tracking-widest text-center border-t border-zinc-100 pt-10">
            © 2024 SARYO SUIHA. ALL RIGHTS RESERVED.
          </div>
        </div>
      </footer>
    </div>
  );
};

export default App;
