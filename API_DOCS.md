# 📡 Super Gestor v2 — Documentação Completa da API

## BASE URL
- **Local:**  `http://localhost:3000/api`
- **Vercel:** `https://seu-app.vercel.app/api`

---

## 🚀 POST /api/launch-campaign
**Cria uma campanha completa do zero (campanha → ad set → copy → criativo → anúncio)**

### Request
```json
{
  "produto":            "Curso de Inglês Online",
  "publico_descricao":  "Adultos 25-45 anos que querem aprender inglês para trabalho",
  "link_url":           "https://seusite.com.br/oferta",
  "page_id":            "123456789",
  "nome_campanha":      "[TOPO] Curso Inglês - Interesses",
  "objetivo":           "conversoes",
  "orcamento_diario":   100,
  "image_url":          "https://seusite.com/imagem-anuncio.jpg",
  "pais":               "BR",
  "idade_min":          25,
  "idade_max":          45,
  "instagram_actor_id": "987654321"
}
```

### Response
```json
{
  "success": true,
  "message": "Campanha criada com sucesso! Revise no Meta Ads antes de ativar.",
  "ids": {
    "campaign_id": "120200000000001",
    "adset_id":    "120200000000002",
    "creative_id": "120200000000003",
    "ad_id":       "120200000000004"
  },
  "audiencia": {
    "descricao":  "Adultos profissionais interessados em idiomas e desenvolvimento pessoal",
    "interesses": ["English language", "Language learning", "Career development"]
  },
  "copy": {
    "headline":     "Fale inglês em 90 dias",
    "primary_text": "Método aprovado por +10.000 alunos. Comece hoje.",
    "description":  "Garanta sua vaga agora",
    "cta":          "LEARN_MORE"
  },
  "log": ["🚀 Iniciando...", "✅ Campanha criada...", "🎉 Sucesso!"]
}
```

---

## 🧪 POST /api/create-ab-test
**Cria teste A/B com múltiplas variações de copy e imagem**

### Request
```json
{
  "produto":               "Consultoria de Marketing",
  "publico_descricao":     "Donos de pequenas empresas",
  "link_url":              "https://seusite.com/contato",
  "page_id":               "123456789",
  "nome_base":             "Consultoria Marketing",
  "objetivo":              "leads",
  "orcamento_diario":      150,
  "image_urls":            [
    "https://seusite.com/img-1.jpg",
    "https://seusite.com/img-2.jpg",
    "https://seusite.com/img-3.jpg"
  ],
  "quantidade_variacoes":  3
}
```

### Response
```json
{
  "success": true,
  "campaign_id": "120200000000010",
  "adset_id":    "120200000000011",
  "variacoes": [
    {
      "variacao":   "A",
      "ad_id":      "120200000000012",
      "estrategia": "Foco em benefício principal",
      "copy": { "headline": "Dobre suas vendas em 60 dias" }
    },
    {
      "variacao":   "B",
      "ad_id":      "120200000000013",
      "estrategia": "Foco em prova social",
      "copy": { "headline": "+500 empresas atendidas" }
    },
    {
      "variacao":   "C",
      "ad_id":      "120200000000014",
      "estrategia": "Urgência e escassez",
      "copy": { "headline": "Últimas 5 vagas este mês" }
    }
  ]
}
```

---

## ⚡ POST /api/optimize-campaigns
**Roda otimização automática: pausa perdedores, escala vencedores**

### Request (regras opcionais)
```json
{
  "rules": {
    "pausar_ctr_abaixo":       1.0,
    "pausar_frequencia_acima": 4.0,
    "pausar_min_impressoes":   1000,
    "escalar_roas_acima":      3.0,
    "escalar_percentual":      0.20,
    "periodo":                 "last_7d"
  }
}
```

### Response
```json
{
  "success": true,
  "timestamp": "2025-01-01T10:00:00Z",
  "campanhas_analisadas": 5,
  "acoes_executadas": 3,
  "acoes": [
    {
      "tipo":        "PAUSA_ANUNCIO",
      "ad_id":       "120200000000020",
      "ad_nome":     "Anúncio Summer | Var A",
      "motivo":      "CTR 0.45% < 1%",
      "metricas":    { "ctr": 0.45, "impressoes": 5000, "gasto": 45.00 }
    },
    {
      "tipo":              "ESCALA_ORCAMENTO",
      "campanha_id":       "120200000000001",
      "motivo":            "ROAS 4.20 ≥ 3.0",
      "orcamento_anterior": "R$ 100.00",
      "orcamento_novo":    "R$ 120.00"
    }
  ],
  "relatorio_ia": "Foram pausados 2 anúncios com baixo CTR e escalado o orçamento de 1 campanha com ROAS acima de 4x. Expectativa de melhora no CPA geral em ~15% nos próximos 3 dias."
}
```

---

## 📊 GET /api/account-performance?periodo=last_30d
**Análise geral de performance da conta com diagnóstico IA**

### Response
```json
{
  "metricas": {
    "periodo":      "last_30d",
    "spend":        4500.00,
    "impressions":  850000,
    "clicks":       12500,
    "ctr":          1.47,
    "cpm":          5.29,
    "cpc":          0.36,
    "roas":         3.2,
    "conversoes":   87,
    "receita":      14400.00
  },
  "diagnostico": {
    "status_geral":          "BOM",
    "score":                 72,
    "principais_problemas":  ["CPM elevado em 2 campanhas", "Frequência alta no conjunto 3"],
    "acoes_prioritarias":    ["Renovar criativos do conjunto 3", "Testar novos públicos", "Criar campanha de remarketing 7d"]
  }
}
```

---

## 📈 POST /api/scale-campaign
**Duplica e escala campanha vencedora**

### Request
```json
{
  "campaign_id":             "120200000000001",
  "multiplicador_orcamento": 1.5,
  "expandir_publico":        true,
  "produto":                 "Curso de Inglês",
  "pais":                    "BR"
}
```

### Response
```json
{
  "success": true,
  "original_campaign_id": "120200000000001",
  "nova_campaign_id":     "120200000000099",
  "orcamento_original":   100.00,
  "orcamento_novo":       150.00,
  "adset_broad_id":       "120200000000100"
}
```

---

## ✍️ POST /api/generate-copy
**Gera copy completa com IA**

### Request
```json
{
  "produto":  "Whey Protein Premium",
  "publico":  "Homens 20-35 anos que treinam musculação",
  "objetivo": "conversoes",
  "tom":      "direto e motivacional"
}
```

### Response
```json
{
  "copy": {
    "headline":     "Músculo em 30 dias. Garantido.",
    "primary_text": "Whey com 27g proteína. Sem desculpas. 🔥",
    "description":  "Frete grátis hoje",
    "cta":          "SHOP_NOW",
    "cta_label":    "Comprar Agora",
    "copy_longa":   "Você treina duro. Mas sem a proteína certa, perde resultado...",
    "hooks":        ["Você ainda usa whey fraco?", "27g de proteína por dose", "Resultado em 30 dias ou devolvo"]
  }
}
```

---

## 🎯 POST /api/build-audience
**Gera targeting automático para Meta Ads**

### Request
```json
{
  "produto":    "academia de ginástica",
  "pais":       "BR",
  "idade_min":  20,
  "idade_max":  50,
  "objetivo":   "leads"
}
```

### Response
```json
{
  "targeting": {
    "geo_locations":     { "countries": ["BR"] },
    "age_min":           20,
    "age_max":           50,
    "interests":         [
      { "id": "6003139266461", "name": "Fitness and wellness" },
      { "id": "6003107902433", "name": "Bodybuilding" }
    ],
    "publisher_platforms": ["facebook", "instagram"]
  },
  "descricao_publico":    "Adultos interessados em fitness e saúde que buscam academia",
  "interesses_sugeridos": ["fitness", "musculação", "academia", "saúde", "esporte"],
  "interesses_encontrados": 4
}
```

---

## 🏆 GET /api/rank-ads/:campaign_id?periodo=last_7d
**Ranking de anúncios: vencedores vs perdedores**

### Response
```json
{
  "vencedores": [
    { "ad_id": "...", "nome": "Anúncio Hook A", "score": 87.5,
      "metricas": { "ctr": 2.3, "roas": 4.1, "spend": 250 } }
  ],
  "perdedores": [
    { "ad_id": "...", "nome": "Anúncio Var C", "score": 12.0,
      "metricas": { "ctr": 0.4, "roas": null, "spend": 80 } }
  ],
  "todos": [...]
}
```

---

## 🖼️ POST /api/creative/upload-url
**Faz upload de imagem para o Meta via URL**

### Request
```json
{ "image_url": "https://seusite.com/banner.jpg" }
```

### Response
```json
{
  "success":    true,
  "image_hash": "abc123def456...",
  "image_url":  "https://seusite.com/banner.jpg"
}
```

---

## ⚙️ REGRAS DE OTIMIZAÇÃO — REFERÊNCIA

| Parâmetro | Padrão | Descrição |
|---|---|---|
| `pausar_ctr_abaixo` | 1.0 | Pausa anúncio se CTR < X% |
| `pausar_frequencia_acima` | 4.0 | Pausa se frequência > X |
| `pausar_min_impressoes` | 1000 | Só pausa se tiver X impressões |
| `pausar_cpa_acima` | null | Pausa se CPA > R$X (desativado) |
| `escalar_roas_acima` | 3.0 | Aumenta budget se ROAS > X |
| `escalar_percentual` | 0.20 | Aumenta X% do orçamento |
| `periodo` | last_7d | Janela de análise |

---

## 🎯 OBJETIVOS SUPORTADOS

| Valor | Equivalente Meta |
|---|---|
| `conversoes` | OUTCOME_SALES |
| `leads` | OUTCOME_LEADS |
| `trafego` | OUTCOME_TRAFFIC |
| `engajamento` | OUTCOME_ENGAGEMENT |
| `reconhecimento` | OUTCOME_AWARENESS |
| `app` | OUTCOME_APP_PROMOTION |
