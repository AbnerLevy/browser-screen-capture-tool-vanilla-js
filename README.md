# 📸 Print Function Browser

> Captura e envio de prints diretamente pelo navegador para agilizar o suporte técnico.

---

## 🚨 Problema

No fluxo do suporte, usuários tinham dificuldade em enviar prints de erros:
- Não sabiam como tirar print
- Não sabiam como salvar a imagem
- Enviavam imagens erradas ou incompletas
- Processo lento e despadronizado

Isso gerava retrabalho e aumentava o tempo de resolução dos chamados.

---

## 💡 Solução

Desenvolvi uma funcionalidade web que permite:
- Capturar a tela diretamente no navegador
- Sem necessidade de salvar imagem na maquina local
- Visualizar o print antes do envio
- Enviar a imagem para o servidor de forma simples

Tudo isso sem depender de ferramentas externas.

---

## ⚙️ Como funciona

1. Usuário clica no botão de captura
2. Seleciona qual aba ou janela vai caputurar
3. O sistema tira um print da tela atual
4. Um modal exibe a pré-visualização da imagem
5. O usuário confirma e envia
6. A imagem é enviada para o servidor

---

## 🖼️ Demonstração

<img width="1260" height="639" alt="Animação" src="https://github.com/user-attachments/assets/3ceb3862-569b-4974-a1b3-de43170a8e24" />


Observações:
- O Index.html é só para demonstração do funcionamento, a idéia é que você implemente apenas o javascript no seu projeto, no seu sistema de suporte e etc
- Botão de envio também não está funcional, é só demonstrativo, utilize ele para implementar o envio real para o seu sistema
- Deploy: https://abnerlevy.github.io/Print-Function-Browser/

---

## 🛠️ Tecnologias utilizadas

- JavaScript
- Funções de Web APIs nativas dos navegadores
