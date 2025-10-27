# Kommo Tag Analytics Widget

Widget de análise de leads por tags ativas para Kommo CRM.

## 📋 Descrição

Este widget exibe um painel visual mostrando a distribuição de leads por tags ativas na sua conta Kommo. O design segue um tema azul escuro profissional com:

- Contador total de tags ativas
- Lista de tags com contagem de leads
- Barras de progresso mostrando distribuição percentual
- Cores personalizadas por tag
- Interface responsiva e elegante

## 📦 Estrutura do Widget

```
widget/
├── manifest.json          # Configuração do widget
├── script.js             # Lógica principal (AMD/RequireJS)
├── style.css             # Estilos (tema azul escuro)
├── index.html            # Preview/teste
├── i18n/                 # Traduções
│   ├── en.json          # Inglês
│   └── pt.json          # Português
├── images/               # Logos (adicionar antes do upload)
└── README.md             # Esta documentação
```

## 🚀 Como Instalar no Kommo

### 1. Preparar os Arquivos

```bash
# Criar arquivo ZIP com a estrutura correta
cd widget
zip -r ../tag-analytics-widget.zip * -x "*.DS_Store" -x "__MACOSX/*"
cd ..
```

**Importante**: Os arquivos devem estar na raiz do ZIP, não dentro de uma pasta.

### 2. Upload no Kommo

1. Acesse sua conta Kommo
2. Vá em **Configurações** → **API** → **Widgets**
3. Clique em **Upload Widget**
4. Selecione o arquivo `tag-analytics-widget.zip`
5. Aguarde o processamento

### 3. Configurar o Widget

Após o upload, configure:

- **Backend URL**: URL do servidor backend (ex: `https://seu-replit.repl.co`)
  - **IMPORTANTE**: Este é o servidor que hospeda a API e processa os dados do Kommo
  - Sem esta URL, o widget não conseguirá carregar dados
- **API Key**: Sua chave de API do Kommo
- **Domain**: Seu domínio Kommo (ex: `seudominio.kommo.com`)
- **Refresh Interval**: Intervalo de atualização em segundos (opcional)

### 4. Ativar nos Cards

1. Abra um card de Lead, Contato ou Empresa
2. Clique no menu de tabs (ícone "...")
3. Selecione **Tag Analytics** para adicionar a tab
4. O widget carregará automaticamente os dados

## 🔧 Configuração da API Backend

O widget precisa de um backend para buscar dados da API Kommo. Este projeto já inclui os endpoints necessários:

### Endpoints Disponíveis

- `GET /api/kommo/tags/statistics` - Retorna estatísticas de tags
- `GET /api/kommo/tags` - Lista todas as tags
- `GET /api/kommo/tags/search?q=query` - Busca tags por nome
- `GET /api/kommo/leads?limit=250` - Lista leads com tags

### Variáveis de Ambiente

Configure no seu servidor:

```env
KOMMO_API_KEY=your_api_key_here
KOMMO_DOMAIN=yourdomain.kommo.com
```

## 📊 Formato dos Dados

O backend retorna estatísticas no formato:

```json
{
  "totalTags": 5,
  "totalLeads": 100,
  "tags": [
    {
      "id": 1234,
      "name": "atendimento humano",
      "color": "#FDB022",
      "leadCount": 46,
      "percentage": 46
    }
  ],
  "othersCount": 0,
  "lastUpdated": "2025-10-27T12:00:00.000Z"
}
```

## 🎨 Personalização

### Cores das Tags

As cores são definidas automaticamente por este algoritmo no `script.js`:

```javascript
var colors = [
  '#FDB022', // Amarelo/Laranja
  '#F5A623', // Laranja
  '#7B8CDE', // Azul/Roxo
  '#A3D977', // Verde Claro
  '#98A2B3', // Cinza/Azul
  '#FF6B9D', // Rosa
  '#50C8FF', // Ciano
  '#FFD93D'  // Amarelo
];
```

Você pode modificar essas cores editando a função `getTagColor()` em `script.js`.

### Tema Visual

O tema azul escuro pode ser customizado editando as variáveis em `style.css`:

```css
.tag-analytics-container {
  background-color: #1a2332;  /* Fundo principal */
  color: #e1e8ed;             /* Texto principal */
}

.tag-total {
  color: #7e8ae6;             /* Cor do número total */
}
```

## 🔍 Card SDK

Este widget implementa o Card SDK do Kommo com os seguintes callbacks:

- **loadPreloadedData()** - Carrega tags iniciais
- **loadElements(type, id)** - Carrega tags vinculadas ao card
- **linkCard(links)** - Vincula/desvincula tags (não usado para analytics)
- **searchDataInCard(query, type, id)** - Busca tags por nome

## 📱 Localizações Suportadas

O widget aparece nas seguintes áreas do Kommo:

- `lcard-0` - Cards de Leads
- `ccard-0` - Cards de Contatos
- `comcard-0` - Cards de Empresas
- `settings` - Página de configurações
- `card_sdk` - Suporte ao Card SDK

## 🐛 Troubleshooting

### Widget não carrega dados

1. Verifique se as credenciais estão corretas nas configurações
2. Confirme que o backend está rodando e acessível
3. Verifique os logs do console do navegador (F12)

### Erro de CORS

Se o widget não consegue acessar o backend:

1. Certifique-se de que o backend aceita requisições do domínio Kommo
2. Configure os headers CORS apropriadamente

### Tags não aparecem

1. Verifique se há leads com tags na sua conta Kommo
2. Confirme que as tags estão ativas
3. Teste o endpoint `/api/kommo/tags/statistics` diretamente

## 📄 Licença

Este widget é fornecido como está para uso com Kommo CRM.

## 🤝 Suporte

Para suporte, entre em contato através do email configurado no `manifest.json`.
