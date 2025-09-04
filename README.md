# 📄 Documentação do Frontend - Sistema Médico APH Exams

## 📋 Índice
1. [Visão Geral](#-visão-geral)
2. [Estrutura do Projeto](#-estrutura-do-projeto)
3. [Funcionalidades](#-funcionalidades)
4. [Configuração e Uso](#-configuração-e-uso)
5. [Componentes e Seções](#-componentes-e-seções)
6. [Integração com API](#-integração-com-api)
7. [Personalização](#-personalização)

## 🏥 Visão Geral

O frontend do Sistema Médico APH Exams é uma aplicação web responsiva desenvolvida em HTML, CSS e JavaScript vanilla que consome a API RESTful do backend. A interface oferece uma experiência moderna e intuitiva para gerenciamento de pacientes, agendamento de exames e monitoramento de atividades do sistema.


## ⚙️ Funcionalidades

### 🔐 Sistema de Autenticação
- Login com usuário e senha
- Armazenamento seguro de token JWT
- Controle de permissões baseado em roles
- Logout automático por expiração de token

### 👥 Gerenciamento de Pacientes
- **Listagem** de pacientes com paginação virtual
- **Busca** por nome, CPF ou tipo de exame
- **Filtros** por status de exame
- **Cadastro** de novos pacientes
- **Edição** de informações existentes
- **Visualização** detalhada de registros

### 📊 Logs do Sistema
- Monitoramento em tempo real de atividades
- Filtros por tipo de ação (INSERT, UPDATE, DELETE)
- Busca textual em detalhes dos logs
- Timestamp com formatação local

### 🎨 Interface do Usuário
- Design responsivo para desktop e mobile
- Feedback visual com alertas contextuais
- Indicadores de status com badges coloridos
- Formatação automática de CPF e telefone
- Validação de formulários no client-side

## 🚀 Configuração e Uso

### Pré-requisitos
- Navegador moderno (Chrome 80+, Firefox 75+, Safari 13+)
- Servidor backend executando na porta 3000

### Instalação Rápida
1. **Salve o arquivo HTML** em seu sistema
   ```bash
   # Salve como frontend.html
   ```

2. **Configure a URL da API** (se necessário)
   ```javascript
   // Edite esta linha no arquivo HTML
   const API_BASE_URL = 'http://localhost:3000'; // URL do seu backend
   ```

3. **Abra no navegador**
   ```bash
   # Método 1: Duplo clique no arquivo
   # Método 2: Servidor local (Python)
   python -m http.server 8000
   # Acesse: http://localhost:8000/frontend.html
   ```

### Usuários de Teste
O sistema inclui usuários predefinidos para teste:

| Usuário     | Senha        | Permissões     |
|-------------|--------------|----------------|
| `admin`     | `admin123`   | Administrador  |
| `medico`    | `medico123`  | Médico         |
| `enfermeiro`| `enfermeiro123` | Enfermeiro    |

## 🧩 Componentes e Seções

### Seção de Login (`#login-section`)
- Formulário de autenticação
- Dicas de usuários de teste
- Validação de campos obrigatórios

### Seção de Pacientes (`#patients-section`)
```javascript
// Estrutura de dados do paciente
{
  id: number,
  name: string,
  cpf: string (formatado),
  birthDate: ISO string,
  motherName: string,
  phone: string,
  examType: string,
  status: 'AGENDADO' | 'REALIZADO' | 'PENDENTE' | 'CANCELADO',
  examDate: ISO string,
  protocol: string
}
```

### Seção de Logs (`#logs-section`)
- Tabela com histórico de ações
- Timestamps convertidos para fuso local
- Filtros por tipo de ação e busca textual

### Sistema de Alertas
```javascript
// Exemplo de uso
showAlert('Operação realizada com sucesso!', 'success');
showAlert('Erro na operação', 'error');
```

## 🔌 Integração com API

### Configuração de Endpoints
```javascript
const ENDPOINTS = {
  login: '/api/auth/login',
  patients: '/api/patients',
  patientDetail: (cpf) => `/api/patients/${cpf}`,
  logs: '/api/logs',
  health: '/api/health'
};
```

### Estrutura das Requisições
```javascript
// Headers automáticos
headers: {
  'Content-Type': 'application/json',
  'Authorization': `Bearer ${token}`
}
```

### Tratamento de Erros
- Alertas visuais para erros de API
- Redirecionamento automático em caso de token expirado
- Fallbacks para dados não disponíveis

## 🎨 Personalização

### Cores e Temas
Modifique as variáveis CSS no início do arquivo:
```css
:root {
  --primary: #2563eb;       /* Cor primária */
  --primary-dark: #1d4ed8;  /* Cor primária escura */
  --secondary: #64748b;     /* Cor secundária */
  --success: #10b981;       /* Cor de sucesso */
  --danger: #ef4444;        /* Cor de erro */
  /* ... outras variáveis */
}
```

### Tipos de Exame Personalizados
Edite o elemento `<select>` com id `examType`:
```html
<option value="NOVO_EXAME">Novo Tipo de Exame</option>
```

### Status Personalizados
Adicione novos status no HTML e CSS:
```html
<option value="NOVO_STATUS">Novo Status</option>
```

```css
.status-novo_status {
  background-color: #cor_desejada;
  color: #cor_texto;
}
```

## 📱 Responsividade

O frontend é totalmente responsivo com breakpoints para:
- **Desktop**: > 1024px
- **Tablet**: 768px - 1024px
- **Mobile**: < 768px

## 🔒 Segurança

- Tokens JWT armazenados em `localStorage`
- Validação de expiração de token
- Sanitização básica de inputs
- Headers de autenticação em todas as requisições

