# Roadmap — Landing Page Cicle Dois Irmãos (Campanha Nova Mobilidade)

Stack escolhido: HTML/CSS/JS puro + Cloudflare Pages (deploy via Git) + formulário via webhook (endpoint a definir).
Domínio final: https://cicledoisirmaos.com.br

Legenda: [ ] pendente · [x] feito · (RM) Roki Media · (CL) cliente/Eduardo

## Fase 0 — Preparação (dia 1)
- [x] Revisar copy, e-book e index.html existente
- [ ] (RM) Criar repositório Git (`landing-cicle`) com `index.html`, `assets/`, `ROADMAP.md`
- [ ] (CL) Enviar o PDF final do e-book (`guia-nova-mobilidade.pdf`)
- [ ] (CL) Enviar acesso ao DNS de cicledoisirmaos.com.br (registro.br ou registrador) — o domínio não resolvia na auditoria de agosto

## Fase 1 — Ajustes na página (dias 1–2)
- [ ] Alinhar headlines por canal (padrão/google/instagram/tiktok) ao documento de copy aprovado
- [ ] Corrigir ícone do botão "Baixar o PDF" (seta invertida)
- [ ] Extrair imagens e fontes Klavika do base64 para `assets/` (meta: página < 350 KB, LCP < 2,5 s no 4G)
- [ ] Converter imagens para WebP/AVIF com `srcset`; `font-display: swap` nas fontes
- [ ] Reativar seção "Para quem é" como bloco próprio (opcional, conforme copy seção 6)
- [ ] Revisar política de privacidade (rascunho no dialog `#privacy`) — (CL) validar texto
- [ ] Adicionar `robots.txt`, `sitemap.xml`, `og:image` (capa 3D do e-book) e favicon em arquivo
- [ ] Página `/obrigado` opcional (URL própria facilita conversão por URL no Google/Meta); hoje o obrigado é inline

## Fase 2 — Captura de lead (dias 2–3) — bloqueado até definir o endpoint
- [ ] (CL) Definir destino do lead: webhook Make/n8n → RAFE, ou URL de captura nativa do RAFE
- [ ] Preencher `CONFIG.endpoint`; garantir CORS no destino
- [ ] Payload já enviado pela página: nome, email, whatsapp, interesses[], consentimento, utm_source/medium/campaign/content/term, gclid/fbclid/ttclid, timestamp
- [ ] Mapear interesses → etiquetas no CRM (7 opções)
- [ ] Cadastrar modelos de mensagem no WhatsApp Business (imediata + follow-up 2 dias) — pode exigir aprovação da Meta
- [ ] Fallback: se o webhook falhar, a página ainda entrega o PDF e loga o erro

## Fase 3 — Rastreamento (dia 3)
- [ ] Instalar GTM no `<head>` (um container para gtag/GA4, Meta Pixel e TikTok Pixel)
- [ ] Mapear eventos já disparados pela página: `generate_lead` (dataLayer/gtag), `fbq('track','Lead')`, `ttq.track('SubmitForm')`, `whatsapp_click`
- [ ] Configurar conversões: Google Ads (generate_lead), Meta (Lead + API de Conversões via Make/n8n), TikTok (SubmitForm)
- [ ] Testar com Tag Assistant / Meta Pixel Helper nos 3 canais com UTM

## Fase 4 — Deploy (dia 4)
- [ ] Criar projeto no Cloudflare Pages conectado ao repositório (branch `main` = produção, PRs = preview)
- [ ] Adicionar domínio customizado `cicledoisirmaos.com.br` + `www` (redirect para apex); HTTPS automático
- [ ] Apontar DNS (nameservers na Cloudflare, ou CNAME no registrador atual)
- [ ] Headers de segurança e cache via `_headers` (CSP permissiva para GTM/pixels, cache longo em `assets/`)
- [ ] Publicar `guia-nova-mobilidade.pdf` na raiz

## Fase 5 — QA e go-live (dia 5)
- [ ] Lighthouse mobile ≥ 90 em performance e acessibilidade
- [ ] Testar formulário nos 3 canais (`?utm_source=google|instagram|tiktok`): lead chega no CRM e no WhatsApp; PDF abre no celular
- [ ] Testar validações (WhatsApp inválido, sem interesse, sem consentimento) e honeypot
- [ ] Checar em iPhone Safari, Android Chrome, desktop
- [ ] (CL) Aprovar página final
- [ ] Apontar os Reels "Precisa de CNH para scooter?" e "Elétrico sem abrir o bolso" para a LP
- [ ] Ligar as campanhas

## Pós-lançamento
- [ ] Semana 1: revisar custo por lead; se acima do alvo, testar remoção do campo e-mail (regra do copy)
- [ ] Inserir prova social quando houver depoimentos autorizados ou nota do Google (remover `hidden` de `#depoimentos`)
- [ ] Reservar selo "60 anos" para 2027 (rodapé e e-book)
- [ ] Se entrar modelo > 1.000 W / 32 km/h na loja, retirar a promessa "sem CNH" da LP e dos anúncios

## Bloqueios atuais (dependem do cliente)
1. PDF do e-book
2. Endpoint do lead (CRM/webhook)
3. IDs de rastreamento (GTM/GA4, Pixel Meta, Pixel TikTok)
4. Acesso ao DNS do domínio
5. Depoimentos ou nota do Google
6. Texto final da política de privacidade
