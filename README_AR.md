# 📱 Como Testar AR no Celular

## ⚠️ PROBLEMA: getUserMedia requer HTTPS

A API de câmera (`getUserMedia`) só funciona em:
- ✅ `https://` (HTTPS)
- ✅ `localhost`
- ❌ `http://` (HTTP) - **NÃO FUNCIONA**

## 🚀 Soluções

### Opção 1: ngrok (Recomendado - Mais Fácil)

1. **Instale o ngrok:**
   ```bash
   # Via npm
   npm install -g ngrok
   
   # Ou baixe: https://ngrok.com/download
   ```

2. **Inicie o servidor Next.js:**
   ```bash
   npm run dev
   ```

3. **Em outro terminal, crie o túnel HTTPS:**
   ```bash
   ngrok http 3000
   ```

4. **Copie o link HTTPS gerado:**
   ```
   Forwarding   https://abc123.ngrok.io -> http://localhost:3000
   ```

5. **Acesse no celular:**
   - Abra o link `https://abc123.ngrok.io/viewer` no Chrome do celular
   - Permita acesso à câmera quando solicitado ✅

---

### Opção 2: Cloudflare Tunnel (Alternativa)

1. **Instale cloudflared:**
   ```bash
   npm install -g cloudflared
   # Ou: brew install cloudflare/cloudflare/cloudflared
   ```

2. **Inicie o servidor:**
   ```bash
   npm run dev
   ```

3. **Crie o túnel:**
   ```bash
   cloudflared tunnel --url http://localhost:3000
   ```

4. **Use o link HTTPS gerado no celular**

---

### Opção 3: Localhost via USB (Celular Android)

1. **Conecte o celular via USB**

2. **Ative depuração USB nas configurações do Android**

3. **Configure port forwarding no Chrome:**
   - Desktop: `chrome://inspect`
   - Clique em "Port forwarding"
   - Adicione: `3000` → `localhost:3000`

4. **No celular, acesse:**
   ```
   http://localhost:3000/viewer
   ```

⚠️ Mesmo assim, alguns navegadores podem bloquear por não ser HTTPS real.

---

## 🧪 Teste Rápido

Para verificar se a câmera vai funcionar:

1. Acesse: `chrome://flags` no Chrome do celular
2. Procure: "Insecure origins treated as secure"
3. Adicione: `http://192.168.15.5:3000`
4. Reinicie o Chrome

⚠️ **Isso é só para testes!** Em produção, sempre use HTTPS.

---

## 📦 Deploy em Produção

Para usar em produção (sempre HTTPS):

- **Vercel:** `vercel deploy` (HTTPS automático)
- **Netlify:** `netlify deploy` (HTTPS automático)
- **Cloudflare Pages:** HTTPS automático
- **Servidor próprio:** Configure certificado SSL/TLS

---

## 🔍 Debug

Se ainda não funcionar, abra o console no celular:

1. Conecte celular via USB
2. Desktop: `chrome://inspect`
3. Clique em "inspect" no seu device
4. Veja os logs de erro

---

## ✅ Checklist

- [ ] Servidor rodando (`npm run dev`)
- [ ] ngrok/cloudflared instalado
- [ ] Túnel HTTPS criado
- [ ] Acesso via link HTTPS no celular
- [ ] Permissão de câmera concedida
- [ ] AR funcionando! 🎉
