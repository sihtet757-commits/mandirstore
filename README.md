: p.title_my  p.title}</h4>
                  <p className="text-sm text-gray-500 mt-1">{lang === "en" ? p.description : p.description_my || p.description}</p>
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
          <div>{© ${new Date().getFullYear()} Sherry Game Store — ${t.tagline}}</div>
          <div className="mt-2">{Website preview for: https://Mandirgamestore.com}</div>
        </footer>
      </main>

      {/* Product Modal */}
      {viewProduct && (
        <div className="fixed inset-0 bg-black/40 flex items-center justify-center p-4">
          <div className="bg-white rounded-lg max-w-3xl w-full overflow-auto">
            <div className="p-4 flex justify-between items-start">
              <h4 className="text-xl font-semibold">{lang === "en" ? viewProduct.title : viewProduct.title_my}</h4>
              <button onClick={() => setViewProduct(null)} className="text-gray-500">✕</button>
            </div>
            <div className="p-4 grid md:grid-cols-2 gap-4">
              <img src={viewProduct.img} alt={viewProduct.title} className="w-full h-64 object-cover rounded" />
              <div>
                <p className="text-gray-600">{lang === "en" ? viewProduct.description : viewProduct.description_my}</p>
                <div className="mt-4 text-lg font-bold">${viewProduct.price.toFixed(2)}</div>
                <div className="mt-4 flex gap-2">
                  <button onClick={() => { addToCart(viewProduct); setViewProduct(null); }} className="px-4 py-2 rounded-lg bg-indigo-600 text-white">{t.addToCart}</button>
                  <button onClick={() => setViewProduct(null)} className="px-4 py-2 rounded-lg border">Close</button>
                </div>
              </div>
            </div>
          </div>
        </div>
      )}

      {/* Checkout drawer/modal */}
      {showCheckout && (
        <div className="fixed inset-0 bg-black/40 flex items-end md:items-center justify-center p-4">
          <div className="bg-white rounded-t-lg md:rounded-lg w-full md:w-3/4 max-w-3xl p-6">
            <div className="flex items-center justify-between mb-4">
              <h4 className="text-lg font-semibold">{t.cart}</h4>
              <button onClick={() => setShowCheckout(false)} className="text-gray-500">✕</button>
            </div>
