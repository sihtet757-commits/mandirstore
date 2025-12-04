import { useState } from "react";

export default function App() {
  const [lang, setLang] = useState("en");
  const [viewProduct, setViewProduct] = useState(null);
  const [showCheckout, setShowCheckout] = useState(false);
  const [cart, setCart] = useState([]);

  const t = {
    viewDetails: lang === "en" ? "View Details" : "အသေးစိတ်ကြည့်မည်",
    addToCart: lang === "en" ? "Add to Cart" : "ကားထဲထည့်မည်",
    cart: lang === "en" ? "Your Cart" : "ဈေးထုပ်",
    tagline: lang === "en" ? "Best price, best quality" : "အကောင်းဆုံးဈေးနှုန်းနဲ့ အရည်အသွေး",
  };

  const products = [
    {
      id: 1,
      title: "PS5 Controller",
      title_my: "PS5 ခလုတ်",
      description: "Brand new original PS5 Controller",
      description_my: "PS5 မူလ ခလုတ်အသစ်",
      price: 85,
      img: "https://i.imgur.com/7yUVEeD.jpeg",
    },
    {
      id: 2,
      title: "Gaming Keyboard",
      title_my: "ဂեյမင်း ကီးဘုတ်",
      description: "RGB Mechanical Keyboard",
      description_my: "RGB မီကန်နစ်ကယ် ကီးဘုတ်",
      price: 45,
      img: "https://i.imgur.com/wt6dB9P.jpeg",
    },
  ];

  const addToCart = (p) => {
    setCart([...cart, p]);
  };

  const total = cart.reduce((sum, i) => sum + i.price, 0);

  return (
    <main className="p-6 max-w-6xl mx-auto">

      {/* Header */}
      <header className="flex justify-between items-center mb-6">
        <h2 className="text-2xl font-bold">Mandir Game Store</h2>

        <div className="flex gap-3">
          <button
            onClick={() => setLang("en")}
            className={`px-3 py-1 border rounded ${lang === "en" && "bg-black text-white"}`}
          >
            EN
          </button>
          <button
            onClick={() => setLang("my")}
            className={`px-3 py-1 border rounded ${lang === "my" && "bg-black text-white"}`}
          >
            MM
          </button>

          <button
            onClick={() => setShowCheckout(true)}
            className="px-3 py-1 bg-indigo-600 text-white rounded"
          >
            {t.cart} ({cart.length})
          </button>
        </div>
      </header>

      {/* Product Grid */}
      <section>
        <div className="grid sm:grid-cols-2 md:grid-cols-3 gap-6">
          {products.map((p) => (
            <article key={p.id} className="border rounded-lg overflow-hidden shadow">
              <img src={p.img} className="w-full h-48 object-cover" />

              <div className="p-4">
                <h4 className="text-lg font-semibold">
                  {lang === "en" ? p.title : p.title_my || p.title}
                </h4>

                <p className="text-gray-500 mt-1">
                  {lang === "en" ? p.description : p.description_my || p.description}
                </p>

                <div className="mt-4 flex items-center justify-between">
                  <div className="text-lg font-bold">${p.price.toFixed(2)}</div>

                  <div className="flex gap-2">
                    <button
                      onClick={() => setViewProduct(p)}
                      className="px-3 py-2 rounded-lg border"
                    >
                      {t.viewDetails}
                    </button>

                    <button
                      onClick={() => addToCart(p)}
                      className="px-3 py-2 rounded-lg bg-indigo-600 text-white"
                    >
                      {t.addToCart}
                    </button>
                  </div>
                </div>
              </div>
            </article>
          ))}
        </div>
      </section>

      {/* Footer */}
      <footer className="mt-12 py-8 text-center text-sm text-gray-500">
        <div>
          © {new Date().getFullYear()} Mandir Game Store — {t.tagline}
        </div>
        <div className="mt-2">
          Website preview for: https://Mandirgamestore.com
        </div>
      </footer>

      {/* Product Modal */}
      {viewProduct && (
        <div className="fixed inset-0 bg-black/40 flex items-center justify-center p-4">
          <div className="bg-white rounded-lg max-w-3xl w-full overflow-auto">
            <div className="p-4 flex justify-between items-start">
              <h4 className="text-xl font-semibold">
                {lang === "en" ? viewProduct.title : viewProduct.title_my}
              </h4>

              <button
                onClick={() => setViewProduct(null)}
                className="text-gray-500"
              >
                ✕
              </button>
            </div>

            <div className="p-4 grid md:grid-cols-2 gap-4">
              <img
                src={viewProduct.img}
                className="w-full h-64 object-cover rounded"
              />

              <div>
                <p className="text-gray-600">
                  {lang === "en"
                    ? viewProduct.description
                    : viewProduct.description_my}
                </p>

                <div className="mt-4 text-lg font-bold">
                  ${viewProduct.price.toFixed(2)}
                </div>

                <div className="mt-4 flex gap-2">
                  <button
                    onClick={() => {
                      addToCart(viewProduct);
                      setViewProduct(null);
                    }}
                    className="px-4 py-2 rounded-lg bg-indigo-600 text-white"
                  >
                    {t.addToCart}
                  </button>

                  <button
                    onClick={() => setViewProduct(null)}
                    className="px-4 py-2 rounded-lg border"
                  >
                    Close
                  </button>
                </div>
              </div>
            </div>

          </div>
        </div>
      )}

      {/* Checkout Drawer */}
      {showCheckout && (
        <div className="fixed inset-0 bg-black/40 flex items-end md:items-center justify-center p-4">

          <div className="bg-white rounded-t-lg md:rounded-lg w-full md:w-3/4 max-w-3xl p-6">
            
            <div className="flex items-center justify-between mb-4">
              <h4 className="text-lg font-semibold">{t.cart}</h4>
              <button
                onClick={() => setShowCheckout(false)}
                className="text-gray-500"
              >
                ✕
              </button>
            </div>

            {cart.length === 0 ? (
              <p className="text-center text-gray-500 py-6">
                Cart is empty
              </p>
            ) : (
              <div>
                {cart.map((item, i) => (
                  <div key={i} className="flex justify-between py-2 border-b">
                    <span>{item.title}</span>
                    <span>${item.price.toFixed(2)}</span>
                  </div>
                ))}

                <div className="mt-4 text-right font-bold text-lg">
                  Total: ${total.toFixed(2)}
                </div>
              </div>
            )}

          </div>
        </div>
      )}

    </main>
  );
} 
