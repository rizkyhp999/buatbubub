"use client";

import { useState, useEffect } from "react";
import { motion, AnimatePresence } from "framer-motion";
import { Heart, Gift, Sparkles, Camera } from "lucide-react";
import Image from "next/image";

interface Memory {
  id: number;
  image: string;
  title: string;
  description: string;
  date: string;
}

const memories: Memory[] = [
  {
    id: 1,
    image: "/1.1.1.webp?height=400&width=400",
    title: "KAMUU CANTIKK BNGTT SYNGGG",
    description:
      "Beneran deh, waktu itu kamu tuh cantiknya nggak masuk akal 😭❤️ Aku nggak bisa berhenti liatin kamu 😳💕",
    date: "💖💘💞💓",
  },

  {
    id: 2,
    image: "/2.2.jpg?height=400&width=400",
    title: "Cuteeeee!",
    description:
      "SUKA BANGET SAMA INII CUTEEE GITUUUU. Meleleh aku mbaaa liatnyaa 😭😭😭",
    date: "(❁´◡`❁)",
  },
  {
    id: 3,
    image: "/1.1.jpg?height=400&width=400",
    title: "Rulistia Amanda",
    description:
      " Bocil 2004 yang petantang petenteng, tapi aku suka banget gaya loe",
    date: "(～￣▽￣)～",
  },
  {
    id: 4,
    image: "/6.jpg?height=400&width=400",
    title: "❤️🩷🧡💛💚💙🩵💜🤎🖤🩶🤍",
    description:
      "Gabisa ngelupain momen ini, walau kamu nyanyi ke seluruh mahasiswa tapi aku tau, kamu nyanyi ini buat aku ",
    date: "[]~(￣▽￣)~*",
  },
  {
    id: 5,
    image: "/12.jpg?height=400&width=400",
    title: "Lucu yahhh yg iniiii",
    description: "Aku ngerasaa foto fotoo kita disini lucuu bangett tauuuu",
    date: "ヾ(＠⌒ー⌒＠)ノ",
  },
  {
    id: 6,
    image: "/2.jpg?height=400&width=400",
    title: "Liat Ekspresi Aku",
    description:
      "Liattt donggg seseneng apaa mukaa akuuu kalau di dekat kamuuu",
    date: "(￣y▽,￣)╭ ",
  },
];

// Predefined positions for sparkles to avoid hydration mismatch
// Predefined positions for sparkles to avoid hydration mismatch
const sparklePositions = Array.from({ length: 50 }, () => ({
  left: `${Math.floor(Math.random() * 90 + 5)}%`,
  top: `${Math.floor(Math.random() * 90 + 5)}%`,
  delay: Math.random() * 5,
  repeatDelay: Math.random() * 3,
}));

export default function BirthdayPage() {
  const [stage, setStage] = useState<"candles" | "gift" | "memories">(
    "candles"
  );
  const [candlesBlown, setCandlesBlown] = useState(false);
  const [giftOpened, setGiftOpened] = useState(false);
  const [selectedMemory, setSelectedMemory] = useState<Memory | null>(null);
  const [showHearts, setShowHearts] = useState(false);
  const [isClient, setIsClient] = useState(false);

  useEffect(() => {
    setIsClient(true);
  }, []);

  useEffect(() => {
    if (candlesBlown) {
      setTimeout(() => setStage("gift"), 2000);
    }
  }, [candlesBlown]);

  useEffect(() => {
    if (giftOpened) {
      setTimeout(() => setStage("memories"), 1500);
    }
  }, [giftOpened]);

  const blowCandles = () => {
    setCandlesBlown(true);
    setShowHearts(true);
    const audio = new Audio("/hbd.m4a");
    audio.play();
  };

  const openGift = () => {
    setGiftOpened(true);
  };

  return (
    <div className="min-h-screen bg-gradient-to-br from-pink-100 via-purple-50 to-indigo-100 overflow-hidden relative">
      {/* Floating Hearts */}
      <AnimatePresence>
        {showHearts && (
          <div className="fixed inset-0 pointer-events-none z-50">
            {[...Array(20)].map((_, i) => (
              <motion.div
                key={i}
                initial={{
                  x: Math.random() * window.innerWidth,
                  y: window.innerHeight + 50,
                  scale: 0,
                }}
                animate={{
                  y: -100,
                  scale: [0, 1, 0],
                  rotate: [0, 180, 360],
                }}
                transition={{
                  duration: 3 + Math.random() * 2,
                  delay: Math.random() * 2,
                  repeat: Number.POSITIVE_INFINITY,
                  repeatDelay: Math.random() * 3,
                }}
                className="absolute"
              >
                <Heart className="w-6 h-6 text-pink-500 fill-pink-500" />
              </motion.div>
            ))}
          </div>
        )}
      </AnimatePresence>

      {/* Sparkles Background - Only render on client side */}
      {isClient && (
        <div className="fixed inset-0 pointer-events-none">
          {sparklePositions.map((pos, i) => (
            <motion.div
              key={i}
              initial={{ opacity: 0 }}
              animate={{
                opacity: [0, 1, 0],
                scale: [0, 1, 0],
              }}
              transition={{
                duration: 2,
                delay: pos.delay,
                repeat: Number.POSITIVE_INFINITY,
                repeatDelay: pos.repeatDelay,
              }}
              className="absolute"
              style={{
                left: pos.left,
                top: pos.top,
              }}
            >
              <Sparkles className="w-4 h-4 text-yellow-400" />
            </motion.div>
          ))}
        </div>
      )}

      <div className="relative z-10">
        {/* Candles Stage */}
        <AnimatePresence>
          {stage === "candles" && (
            <motion.div
              initial={{ opacity: 0 }}
              animate={{ opacity: 1 }}
              exit={{ opacity: 0, scale: 0.8 }}
              className="min-h-screen flex flex-col items-center justify-center p-4"
            >
              <motion.div
                initial={{ y: 50, opacity: 0 }}
                animate={{ y: 0, opacity: 1 }}
                transition={{ delay: 0.5 }}
                className="text-center mb-8"
              >
                <h1 className="text-6xl md:text-8xl font-bold bg-gradient-to-r from-pink-500 via-purple-500 to-indigo-500 bg-clip-text text-transparent mb-4">
                  Happy 21st
                </h1>
                <h2 className="text-4xl md:text-6xl font-bold text-purple-800 mb-2">
                  Birthday
                </h2>
                <h3 className="text-3xl md:text-5xl font-script text-pink-600">
                  Tia Sayang ✨
                </h3>
              </motion.div>

              {/* Birthday Cake */}
              <motion.div
                initial={{ scale: 0 }}
                animate={{ scale: 1 }}
                transition={{ delay: 1, type: "spring", bounce: 0.5 }}
                className="relative mb-8 mt-10"
              >
                <div className="w-64 h-48 bg-gradient-to-t from-pink-300 to-pink-200 rounded-t-full relative shadow-2xl">
                  {/* Cake Layers */}
                  <div className="absolute bottom-0 w-full h-16 bg-gradient-to-t from-pink-400 to-pink-300 rounded-b-lg"></div>
                  <div className="absolute bottom-16 w-56 h-12 bg-gradient-to-t from-purple-300 to-purple-200 rounded-lg left-4"></div>

                  {/* Candles */}
                  <div className="absolute -top-8 left-1/2 transform -translate-x-1/2 flex space-x-4">
                    {[1, 2].map((candle) => (
                      <div key={candle} className="relative">
                        <div className="w-2 h-8 bg-yellow-200 rounded-sm"></div>
                        <motion.div
                          animate={
                            candlesBlown
                              ? { scale: 0, opacity: 0 }
                              : { scale: [1, 1.2, 1] }
                          }
                          transition={{
                            duration: 0.5,
                            repeat: candlesBlown ? 0 : Number.POSITIVE_INFINITY,
                          }}
                          className="absolute -top-2 left-1/2 transform -translate-x-1/2"
                        >
                          <div className="w-3 h-3 bg-orange-400 rounded-full shadow-lg"></div>
                          <div className="w-1 h-2 bg-orange-500 rounded-full mx-auto"></div>
                        </motion.div>
                      </div>
                    ))}
                  </div>
                </div>
              </motion.div>

              {!candlesBlown && (
                <motion.button
                  initial={{ y: 20, opacity: 0 }}
                  animate={{ y: 0, opacity: 1 }}
                  transition={{ delay: 2 }}
                  whileHover={{ scale: 1.05 }}
                  whileTap={{ scale: 0.95 }}
                  onClick={blowCandles}
                  className="px-8 py-4 bg-gradient-to-r from-pink-500 to-purple-500 text-white font-bold text-xl rounded-full shadow-lg hover:shadow-xl transition-all duration-300"
                >
                  🎂 Tiup Lilinnya! 🎂
                </motion.button>
              )}

              {candlesBlown && (
                <motion.div
                  initial={{ opacity: 0, y: 20 }}
                  animate={{ opacity: 1, y: 0 }}
                  className="text-center"
                >
                  <h4 className="text-2xl font-bold text-purple-800 mb-2">
                    Selamat Ulang Tahun Sayang! 💕
                  </h4>
                  <p className="text-lg text-purple-600">
                    Ada kejutan untukmu...
                  </p>
                </motion.div>
              )}
            </motion.div>
          )}
        </AnimatePresence>

        {/* Gift Stage */}
        <AnimatePresence>
          {stage === "gift" && (
            <motion.div
              initial={{ opacity: 0 }}
              animate={{ opacity: 1 }}
              exit={{ opacity: 0 }}
              className="min-h-screen flex flex-col items-center justify-center p-4"
            >
              <motion.div
                initial={{ y: 50, opacity: 0 }}
                animate={{ y: 0, opacity: 1 }}
                className="text-center mb-8"
              >
                <h2 className="text-4xl md:text-6xl font-bold text-purple-800 mb-4">
                  Ada Hadiah Untukmu! 🎁
                </h2>
                <p className="text-xl text-purple-600">
                  Klik kotak hadiah untuk membukanya
                </p>
              </motion.div>

              <motion.div
                initial={{ scale: 0, rotate: -180 }}
                animate={{ scale: 1, rotate: 0 }}
                transition={{ type: "spring", bounce: 0.6, duration: 1 }}
                className="relative cursor-pointer"
                onClick={openGift}
              >
                <motion.div
                  whileHover={{ scale: 1.05, rotate: [0, -5, 5, 0] }}
                  whileTap={{ scale: 0.95 }}
                  className="relative"
                >
                  {/* Gift Box */}
                  <div className="w-48 h-48 bg-gradient-to-br from-red-400 to-red-600 rounded-lg shadow-2xl relative overflow-hidden">
                    {/* Gift Wrap Pattern */}
                    <div className="absolute inset-0 opacity-20">
                      <div
                        className="w-full h-full bg-red-300"
                        style={{
                          backgroundImage: `repeating-linear-gradient(45deg, transparent, transparent 10px, rgba(255,255,255,0.1) 10px, rgba(255,255,255,0.1) 20px)`,
                        }}
                      ></div>
                    </div>

                    {/* Ribbon Vertical */}
                    <div className="absolute left-1/2 transform -translate-x-1/2 w-8 h-full bg-gradient-to-b from-yellow-300 to-yellow-500"></div>

                    {/* Ribbon Horizontal */}
                    <div className="absolute top-1/2 transform -translate-y-1/2 w-full h-8 bg-gradient-to-r from-yellow-300 to-yellow-500"></div>

                    {/* Bow */}
                    <motion.div
                      animate={giftOpened ? { scale: 0, rotate: 360 } : {}}
                      className="absolute -top-4 left-1/2 transform -translate-x-1/2"
                    >
                      <div className="w-16 h-12 bg-gradient-to-b from-yellow-300 to-yellow-500 rounded-full relative">
                        <div className="absolute inset-2 bg-yellow-400 rounded-full"></div>
                        <div className="absolute top-1/2 left-1/2 transform -translate-x-1/2 -translate-y-1/2 w-2 h-8 bg-yellow-600 rounded-full"></div>
                      </div>
                    </motion.div>

                    {/* Gift Icon */}
                    <div className="absolute inset-0 flex items-center justify-center">
                      <Gift className="w-16 h-16 text-white opacity-30" />
                    </div>
                  </div>

                  {giftOpened && (
                    <motion.div
                      initial={{ scale: 0, opacity: 0 }}
                      animate={{ scale: 1, opacity: 1 }}
                      className="absolute inset-0 flex items-center justify-center"
                    >
                      <div className="w-48 h-48 bg-gradient-to-br from-pink-200 to-purple-200 rounded-lg flex items-center justify-center">
                        <Camera className="w-20 h-20 text-purple-600" />
                      </div>
                    </motion.div>
                  )}
                </motion.div>
              </motion.div>

              {giftOpened && (
                <motion.div
                  initial={{ opacity: 0, y: 20 }}
                  animate={{ opacity: 1, y: 0 }}
                  transition={{ delay: 0.5 }}
                  className="text-center mt-8"
                >
                  <h4 className="text-2xl font-bold text-purple-800 mb-2">
                    Koleksi Kenangan Kita Bersama 📸
                  </h4>
                  <p className="text-lg text-purple-600">
                    Setiap foto menyimpan cerita indah kita...
                  </p>
                </motion.div>
              )}
            </motion.div>
          )}
        </AnimatePresence>

        {/* Memories Stage */}
        <AnimatePresence>
          {stage === "memories" && (
            <motion.div
              initial={{ opacity: 0 }}
              animate={{ opacity: 1 }}
              className="min-h-screen p-4 m-10"
            >
              <motion.div
                initial={{ y: -50, opacity: 0 }}
                animate={{ y: 0, opacity: 1 }}
                className="text-center mb-12 pt-8"
              >
                <h2 className="text-4xl md:text-6xl font-bold bg-gradient-to-r from-pink-500 via-purple-500 to-indigo-500 bg-clip-text text-transparent mb-4">
                  Buat Pacar Aku
                  <br />
                  Rulistia Amanda
                </h2>
                <p className="text-xl text-purple-600 max-w-4xl mx-auto ">
                  Happy Birthday
                </p>
              </motion.div>

              {/* Photo Gallery */}
              <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8 max-w-7xl mx-auto">
                {memories.map((memory, index) => (
                  <motion.div
                    key={memory.id}
                    initial={{ opacity: 0, y: 50, scale: 0.8 }}
                    animate={{ opacity: 1, y: 0, scale: 1 }}
                    transition={{ delay: index * 0.2 }}
                    whileHover={{ scale: 1.05, y: -10 }}
                    className="bg-white rounded-2xl shadow-xl overflow-hidden cursor-pointer"
                    onClick={() => setSelectedMemory(memory)}
                  >
                    <div className="relative h-64 overflow-hidden">
                      <Image
                        src={memory.image || "/placeholder.svg"}
                        alt={memory.title}
                        fill
                        className="object-cover transition-transform duration-300 hover:scale-110"
                      />
                      <div className="absolute inset-0 bg-gradient-to-t from-black/50 to-transparent"></div>
                      <div className="absolute bottom-4 left-4 right-4">
                        <h3 className="text-white font-bold text-lg mb-1">
                          {memory.title}
                        </h3>
                        <p className="text-white/80 text-sm">{memory.date}</p>
                      </div>
                    </div>
                    <div className="p-6">
                      <p className="text-gray-600 line-clamp-3">
                        {memory.description}
                      </p>
                    </div>
                  </motion.div>
                ))}
              </div>

              {/* Final Message */}
              <motion.div
                initial={{ opacity: 0, y: 50 }}
                animate={{ opacity: 1, y: 0 }}
                transition={{ delay: 1.5 }}
                className="text-center mt-16 mb-8"
              >
                <div className="bg-white/80 backdrop-blur-sm rounded-3xl p-8 max-w-4xl mx-auto shadow-2xl">
                  <h3 className="text-3xl md:text-4xl font-bold text-purple-800 mb-6">
                    Untuk Bubub Tersayang 💖
                  </h3>
                  <p className="text-lg text-gray-700 leading-relaxed mb-6">
                    Ciee yang bertambah umurnya, ga kerasa tahun ini udah 21
                    tahun ajaa, semogaaa di usia yang baruu ini kamuu makin
                    bahagiaa, makin sehattt, makin disayang sama banyak orangg,
                    terutama akuuu hehehehehe 💕🎂💖✨
                  </p>

                  <p className="text-lg text-gray-700 leading-relaxed mb-6">
                    Jangan capek yaa jadi orang baikk, karena kamuu udah luar
                    biasa banget sayang. Semoga semuaa hal yang kamu impiin
                    pelan pelan jadi kenyataan yaa sayang. Aku juga berharap
                    diusia baru kamu ini jugaa kamuu makin kuat menghadapi keras
                    dan lembutnya hidupp, semakin dewasaa dalam segala hall,
                    semakin bijak dan semakin cintaa akuuu mwhehehehe. Akuu
                    bangga, aku sayangg, dan selaluu dukung kamuu{" "}
                  </p>
                  <p className="text-2xl font-bold text-pink-600">
                    Selamat Ulang Tahun, Sayang! 🎉✨
                  </p>
                  <p className="text-lg text-purple-600 mt-4">
                    I Love You More Than Words Can Say 💕
                  </p>
                </div>
              </motion.div>
            </motion.div>
          )}
        </AnimatePresence>

        {/* Memory Modal */}
        <AnimatePresence>
          {selectedMemory && (
            <motion.div
              initial={{ opacity: 0 }}
              animate={{ opacity: 1 }}
              exit={{ opacity: 0 }}
              className="fixed inset-0 bg-black/80 backdrop-blur-sm z-50 flex items-center justify-center p-4"
              onClick={() => setSelectedMemory(null)}
            >
              <motion.div
                initial={{ scale: 0.8, opacity: 0 }}
                animate={{ scale: 1, opacity: 1 }}
                exit={{ scale: 0.8, opacity: 0 }}
                className="bg-white rounded-3xl max-w-2xl w-full max-h-[90vh] overflow-y-auto"
                onClick={(e) => e.stopPropagation()}
              >
                <div className="relative h-80">
                  <Image
                    src={selectedMemory.image || "/placeholder.svg"}
                    alt={selectedMemory.title}
                    fill
                    className="object-cover rounded-t-3xl"
                  />
                  <button
                    onClick={() => setSelectedMemory(null)}
                    className="absolute top-4 right-4 w-10 h-10 bg-white/80 backdrop-blur-sm rounded-full flex items-center justify-center text-gray-600 hover:bg-white transition-colors"
                  >
                    ✕
                  </button>
                </div>
                <div className="p-8">
                  <h3 className="text-2xl font-bold text-purple-800 mb-2">
                    {selectedMemory.title}
                  </h3>
                  <p className="text-purple-600 mb-4">{selectedMemory.date}</p>
                  <p className="text-gray-700 leading-relaxed text-lg">
                    {selectedMemory.description}
                  </p>
                </div>
              </motion.div>
            </motion.div>
          )}
        </AnimatePresence>
      </div>
    </div>
  );
}
