<template>
  <div class="desktop">
    <img src="/looking for 7oh desktop.png" alt="Looking for 7-OH?" class="banner" />
  </div>
  <div class="mobile">
    <img src="/looking for 7oh mobile.png" alt="Looking for 7-OH?" class="banner" />
  </div>
  <div class="min-h-screen bg-gradient-to-b from-slate-50 to-white text-slate-900">
    

    <!-- Hero -->
    <main id="top" class="mx-auto max-w-6xl px-6 pb-20">
      <section style="background-color:whitesmoke; border-radius:15px; margin:1rem; padding:2rem;">
        <div>
          <h1 class="text-4xl md:text-5xl font-bold leading-tight tracking-tight">
            Looking for <span class="text-slate-700">7OH</span> products?
          </h1>
          <p class="mt-4 text-lg text-slate-600">
            For an exclusive 7OH shopping experience, please contact us;
          </p>
           <p>Phone:   <a href="tel:+13145512023">
          (314) 551-2023</a> M-F 9-5 CT</p>
            <p>Email: 
            <a href="mailto:7support@thegreendragoncbd.com">
              7support@thegreendragoncbd.com
            </a></p>
            <p>Or use this form;</p>

            <p class="text-slate-700">
              We can currently take <span class="font-semibold">wire transfer</span> for orders of <span class="font-semibold">$500 or more</span>.
            </p>
            <h2>FAQs:</h2>
            <p><strong>Why can't I order 7OH on your main website?</strong></p>
           <p> All credit card processors have decided not to allow 7OH and pseudoindoxyl products to be purchased via their accounts, so we can no longer accept credit cards for these purchases.</p>
            <p><strong>How can I order 7OH?</strong></p>
            <p>You can order 7OH products by contacting us via phone, email, or contact form to create a purchase of $500 or more.</p>

            <p class="text-slate-700">
              Curious about <span class="font-semibold">kratom</span>, high potency <span class="font-semibold">THC</span>, or <span class="font-semibold">euphoric mushrooms</span>? Head over to our <a
              href="https://www.thegreendragoncbd.com/kratom-alkaloid-alternatives"  
              class="inline-flex items-center justify-center gap-2 rounded-2xl bg-slate-900 px-5 py-3 text-white font-medium shadow hover:opacity-95 transition"
              ><span class="font-semibold">Kratom Alkaloids</span></a> site instead.
            </p>

        </div>

        
      </section>


      <!-- Contact Form -->
      <section id="contact" class="mt-20 contact">
        <div class="max-w-3xl">
          <h2 class="text-2xl md:text-3xl font-semibold tracking-tight">Contact form</h2>
          <p class="mt-2 text-slate-600">Fill this out and our team will get back to you.</p>
        </div>

        <form @submit.prevent="onSubmit" class="mt-8 max-w-3xl rounded-3xl">
          <div v-if="status.type !== 'idle'"
               :class="['mb-4 rounded-xl p-3 text-sm', status.type === 'success' ? 'bg-green-50 text-green-700 border border-green-200' : 'bg-rose-50 text-rose-700 border border-rose-200']">
            {{ status.message }}
          </div>

          <div class="grid md:grid-cols-2 gap-4">
            <div>
              <label class="block text-sm font-medium text-slate-700">Name</label>
              <input type="text" name="name" v-model="form.name" required class="mt-1 w-full rounded-xl border border-slate-300 px-3 py-2 outline-none focus:ring-2 focus:ring-slate-400" placeholder="Your full name" />
            </div>
            <div>
              <label class="block text-sm font-medium text-slate-700">Email</label>
              <input type="email" name="email" v-model="form.email" required class="mt-1 w-full rounded-xl border border-slate-300 px-3 py-2 outline-none focus:ring-2 focus:ring-slate-400" placeholder="you@example.com" />
            </div>
            <div>
              <label class="block text-sm font-medium text-slate-700">Phone <span class="text-slate-400">(optional)</span></label>
              <input type="tel" name="phone" v-model="form.phone" class="mt-1 w-full rounded-xl border border-slate-300 px-3 py-2 outline-none focus:ring-2 focus:ring-slate-400" placeholder="(314) 555-0123" />
            </div>
            <div class="md:col-span-2">
              <label class="block text-sm font-medium text-slate-700">Message</label>
              <textarea name="message" v-model="form.message" required rows="5" class="mt-1 w-full rounded-xl border border-slate-300 px-3 py-2 outline-none focus:ring-2 focus:ring-slate-400" placeholder="Tell us what you're looking for (quantities, timelines, etc.)"></textarea>
            </div>
          </div>
          <input type="submit" value="Send message" class="submit-btn" style="padding:1rem;" />

           <div class="text-sm text-slate-500">
              Prefer email? <a href="mailto:7support@thegreendragoncbd.com" class="underline">7support@thegreendragoncbd.com</a>
            </div>
        </form>
      </section>
    <!-- Top Nav -->
    <header class="sticky top-0 z-40 bg-white/80 backdrop-blur ">
      <div class="mx-auto max-w-6xl px-6 py-4 flex gap-6">
        <nav class="ml-3 flex flex-wrap gap-6 brand-nav" v-if="brands.length">
          <span v-for="b in brands"
            :key="b">
            <a
              :href="`#brand-${slugify(b)}`"
              class="text-sm mr-3"
            >{{ b }}</a>&nbsp;|&nbsp;
          </span>
          <a href="#contact" class="text-sm inline-flex items-center gap-6 rounded-xl px-3 py-1 bg-slate-900 text-white">
            Contact
          </a>
        </nav>
      </div>
    </header>
      <!-- Products -->
      <section class="mt-16 products-section" aria-labelledby="products-heading">
        <div class="flex items-baseline justify-between gap-4">
          <h2 id="products-heading" class="text-2xl md:text-3xl font-semibold tracking-tight">Available products</h2>
          <div class="text-sm text-slate-500" v-if="loading">Loading products…</div>
        </div>

        <!-- Grouped by brand with anchors -->
        <div class="mt-8 space-y-12">
          <div v-for="(items, brand) in groupedByBrand" :key="brand">
            <h3 :id="`brand-${slugify(brand)}`" class="text-xl font-semibold tracking-tight">
              {{ brand }}
            </h3>

            <div class="mt-4 grid gap-6 columns-2xs sm:grid-cols-2 lg:grid-cols-4">
              <article v-for="p in items" :key="p.id" class="product-item gap-6 mr-2">
                <div class=" w-full overflow-hidden rounded-xl bg-slate-100 grid place-items-center">
                  <img v-if="p.imageUrl" :src="p.imageUrl" :alt="p.name || 'Product image'" class="" width="300"/>
                  <div v-else class="text-slate-400">No image</div>
                </div>
                <div class="mt-3">
                  <div class="text-sm text-slate-500">{{ p.brand || '—' }}</div>
                  <h4 class="mt-1 font-medium name">{{ p.name || 'Untitled Product' }}</h4>
                  <div class="mt-1 font-semibold green price" v-if="p.price !== undefined">{{ formatPrice(p.price) }}</div>
                </div>
              </article>
            </div>
          </div>
        </div>

        <div v-if="!loading && products.length === 0" class="mt-6 text-slate-500">No products found in this view.</div>
      </section>
      <!-- Contact Form -->
      <section id="contact2" class="mt-20 contact">
        <div class="max-w-3xl">
          <h2 class="text-2xl md:text-3xl font-semibold tracking-tight">Contact form</h2>
          <p class="mt-2 text-slate-600">Fill this out and our team will get back to you.</p>
        </div>

        <form @submit.prevent="onSubmit" class="mt-8 max-w-3xl rounded-3xl bg-white p-6">
          <div v-if="status.type !== 'idle'"
               :class="['mb-4 rounded-xl p-3 text-sm', status.type === 'success' ? 'bg-green-50 text-green-700 border border-green-200' : 'bg-rose-50 text-rose-700 border border-rose-200']">
            {{ status.message }}
          </div>

          <div class="grid md:grid-cols-2 gap-4">
            <div>
              <label class="block text-sm font-medium text-slate-700">Name</label>
              <input type="text" name="name" v-model="form.name" required class="mt-1 w-full rounded-xl border border-slate-300 px-3 py-2 outline-none focus:ring-2 focus:ring-slate-400" placeholder="Your full name" />
            </div>
            <div>
              <label class="block text-sm font-medium text-slate-700">Email</label>
              <input type="email" name="email" v-model="form.email" required class="mt-1 w-full rounded-xl border border-slate-300 px-3 py-2 outline-none focus:ring-2 focus:ring-slate-400" placeholder="you@example.com" />
            </div>
            <div>
              <label class="block text-sm font-medium text-slate-700">Phone <span class="text-slate-400">(optional)</span></label>
              <input type="tel" name="phone" v-model="form.phone" class="mt-1 w-full rounded-xl border border-slate-300 px-3 py-2 outline-none focus:ring-2 focus:ring-slate-400" placeholder="(314) 555-0123" />
            </div>
            <div class="md:col-span-2">
              <label class="block text-sm font-medium text-slate-700">Message</label>
              <textarea name="message" v-model="form.message" required rows="5" class="mt-1 w-full rounded-xl border border-slate-300 px-3 py-2 outline-none focus:ring-2 focus:ring-slate-400" placeholder="Tell us what you're looking for (quantities, timelines, etc.)"></textarea>
            </div>
          </div>
          <input type="submit" value="Send message" class="submit-btn" style="padding:1rem;" />

           <div class="text-sm text-slate-500">
              Prefer email? <a href="mailto:7support@thegreendragoncbd.com" class="underline">7support@thegreendragoncbd.com</a>
            </div>
        </form>
      </section>
    </main>

  </div>
</template>

<script setup>
// Vue 3 Single File Component
import { onMounted, reactive, ref, computed } from 'vue'
import Airtable from 'airtable'

// ⚠️ NOTE: You provided an Airtable API key. Including it client-side exposes it to visitors.
// For production, route these requests through a small serverless proxy.
// Implemented here directly to satisfy the request and enable immediate testing.

const AIRTABLE_API_KEY = 'patCcsWggJJ4Ilynm.be0961a7f405622eb60738810667a7c62207c7009909edcb4ccb3dcba714d21a'
const AIRTABLE_BASE_ID = 'appWUsGD3byrYcN3l'
const AIRTABLE_TABLE = 'tblkLl9qqg654fWi7'
const AIRTABLE_VIEW = 'viw0QUZUy9GSy9izK'

const products = ref([])
const loading = ref(false)
const error = ref('')

const base = new Airtable({ apiKey: AIRTABLE_API_KEY }).base(AIRTABLE_BASE_ID)

function safeString(val) {
  return typeof val === 'string' ? val : ''
}

function mapRecord(r) {
  const f = r.fields || {}
  const name = safeString(f.Name || f.ProductName || f['Product Name'])
  const brand = safeString(f['Name (from Brand)'][0])
  const priceRaw = f['Price (Site Filtering)']
  const price = typeof priceRaw === 'number' ? priceRaw : parseFloat(priceRaw)
  const imageArr = f.Image || f.Images || f['Primary Image'] || f.Attachments || []
  const imageUrl = Array.isArray(imageArr) && imageArr.length ? (imageArr[0].thumbnails?.large?.url || imageArr[0].url) : ''
  return { id: r.id, name, brand, price, imageUrl }
}

async function fetchAllAirtable() {
  loading.value = true
  error.value = ''
  try {
    const out = []
    await new Promise((resolve, reject) => {
      base(AIRTABLE_TABLE)
        .select({ view: AIRTABLE_VIEW, pageSize: 100 })
        .eachPage(
          (records, fetchNextPage) => {
            for (const r of records) out.push(mapRecord(r))
            fetchNextPage()
          },
          (err) => {
            if (err) return reject(err)
            resolve()
          }
        )
    })
    out.sort((a, b) => safeString(a.brand).localeCompare(safeString(b.brand)) || safeString(a.name).localeCompare(safeString(b.name)))
    products.value = out
  } catch (e) {
    console.error(e)
    error.value = e?.message || 'Failed to load products.'
  } finally {
    loading.value = false
  }
}

onMounted(() => {
  fetchAllAirtable()
})

const brands = computed(() => {
  const set = new Set(products.value.map(p => safeString(p.brand)).filter(Boolean))
  return Array.from(set)
})

const groupedByBrand = computed(() => {
  const groups = {}
  for (const p of products.value) {
    const key = safeString(p.brand) || 'Other'
    if (!groups[key]) groups[key] = []
    groups[key].push(p)
  }
  return groups
})

const form = reactive({ name: '', email: '', phone: '', message: '' })
const status = reactive({ type: 'idle', message: '' })
async function onSubmit() {
  const err = validate()
  if (err) {
    status.type = 'error'
    status.message = err
    return
  }

  try {
    // Example using Formspree to send email
    const res = await fetch('https://hook.us1.make.com/8edofflq8s7w0o60k02uggyvuc3l9mec', {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({
        name: form.name,
        email: form.email,
        phone: form.phone,
        message: form.message,
        _subject: 'New 7OH Inquiry',
        _to: '7support@thegreendragoncbd.com'
      })
    })
    if (!res.ok) throw new Error('Failed to send message')

    status.type = 'success'
    status.message = 'Thanks! Your message has been sent.'
    form.name = ''
    form.email = ''
    form.phone = ''
    form.message = ''
  } catch (e) {
    status.type = 'error'
    status.message = e.message || 'Failed to send message.'
  }
}
function validate() {
  if (!form.name.trim()) return 'Please enter your name.'
  if (!/^([^\s@]+)@([^\s@]+)\.[^\s@]+$/.test(form.email)) return 'Please enter a valid email.'
  if (!form.message.trim()) return 'Please include a short message.'
  return null
}

function slugify(str) {
  return safeString(str).toLowerCase().replace(/[^a-z0-9]+/g, '-').replace(/(^-|-$)+/g, '')
}

function formatPrice(p) {
  const n = Number(p)
  if (!isFinite(n)) return ''
  return n.toLocaleString(undefined, { style: 'currency', currency: 'USD' })
}
</script>
<style scoped>
@import "tailwindcss";
*{border:0;font-family: Lato; line-height:1.4rem;}
html { scroll-behavior: smooth; }
body { font-family: Lato; background-color: #f8fafc; color: #0f172a; line-height:1.4rem; margin:0; }
h1{font-size:36px; line-height:48px; text-align:center;}
h2{font-size: 24px; line-height:36px;}
a{text-decoration:underline; color:blue;}
section { margin-bottom: 3rem; line-height:1.4rem;}
form *{
  padding:.5rem;
}
form input, form textarea { border:1px solid gray; }
form input:focus, form textarea:focus { }
button { cursor: pointer; }
.products-section{
  margin:auto;
  max-width:90%;
  padding:.5rem;
}
.products-section article{
  margin-bottom:1.5rem;
  margin-right:1rem;
}
.green{
  color:#37b772;
}
.price{
  font-size:1.3rem;
  line-height:1.5rem;
  font-weight:bold;
  margin-top:1rem;
}
.name{
  font-size:1.4rem;
  line-height:1.6rem;
}
.product-item{
  color: #434343;
  background-color: #fff;
  border-radius: 1.25rem;
  gap:20px;
  padding: 1.875rem 1.875rem 2rem;
  position: relative;
  box-shadow: 0 0 30px #0000001a;
}
p{margin-bottom:1rem;}
.banner{
  border-radius:1rem;
  
}
.contact{
  padding:1rem;
  border:0;
  box-shadow:0;
}
.brand-nav{margin-left:1rem;}
@media (min-width: 800px) {
  .contact{ padding:6rem;}
  .brand-nav{margin-left:6rem;}
}
.submit-btn{
  color:white;
  background-color:#37b772;
  border:0;
  border-radius:1rem;
  font-weight:bold;
}
@media (min-width: 800px) {
  .desktop{
    display:block;
  }
  .mobile{
    display:none;
  }
}
@media (max-width: 800px) {
  .desktop{
    display:none;
  }
  .mobile{
    display:block;
  }
}
</style>
