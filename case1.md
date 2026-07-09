# Enunciado

## Descrição do problema:
- startup de RH, 3 anos, expansão comercial
- contratos enviados pelo cliente, 3 a 4 por semana, em expansão
- problema: startup recebe o contrato e precisa ler do zero, não tem escala
- LegalX já tem banco de cláusulas - classificados em aceitável, negociável e inaceitável -> não estruturado (experiências pessoais, e-mails e mensagens)
- **Objetivo:** tornar o fluxo mais inteligente, usando IA
- **Métricas:** rápido, consistente, independente de supervisão humana

# Solução 

## Objetos necessários:
1) Banco de cláusulas estruturada: nome, conteúdo, margem de aceitação
2) Leitor do contrato enviado: separar as cláusulas e classificar cada uma (aceitável | negociável | inaceitável )
3) Relatório final

## Uso de IA (chatGPT - pessoal)

### Criação de projeto com a descrição:
Quero criar um produto que realize a análise de contratos de prestação de serviços de RH para terceiros e classifique as cláusulas de acordo com banco de dados que possuo. Em seguida, analise cada uma e faça uma nova análise. Não iremos mexer nos códigos nesse momento, apenas analisar o funcionamento.

### Conversa 1
https://chatgpt.com/share/6a4eb1d0-a8fc-83e9-b2fd-fb77db117062

OBS: não conheço um contrato de RH, pedi para a IA organizar as cláusulas necessárias e já fazer essa classificação. Em um caso real, como mencionado no enunciado, essa etapa seria realizada com entrevistas e análise dos textos.


## Script

1) Recebe o documento.
Premissas: 
- é um .pdf
- está em OCR
- sem imagens

2) Chama a IA via API
- passa o JSON na janela de contexto
- prompt: "Faça a classificação do documento enviado conforme o clausulas.json."
- saída estruturada:
[{
    "nome":
    "classificacao":
    "justificativa":
}]

3) Relatório final
- imprimir em formado .pdf

Exemplo: 

**Nome do documento**
| Cláusula | Situação | Justificativa |
| --- | --- | --- |
| Partes | aceitável | Qualificação suficiente para identificar ambas as partes |
| Objeto do Contrato | aceitável | Escopo claramente definido |
| Obrigações | inaceitável | Ausência de deveres mínimos |
| ... | ... | ... |

# Desdobramentos futuros

- O JSON atual deve virar a base do RAG interno. Quando a IA encontrar cláusulas não existentes nele faz a sugestão para o incremento e avisa o advogado responsável para configurar a avaliação.
- Um módulo de extração de PDF para texto pode ser usado por vários produtos, vale a pena transformar em uma API separada para reaproveitamento.
