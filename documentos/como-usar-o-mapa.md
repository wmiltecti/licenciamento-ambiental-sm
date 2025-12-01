Como Usar:
URL atual:

# Ver apenas Imóvel
https://geofront-frontend.onrender.com/index-refactored-ro.html?processo=PROC-2024-002&context=imovel

# Ver apenas Empreendimento
https://geofront-frontend.onrender.com/index-refactored-ro.html?processo=PROC-2024-002&context=empreendimento

# Ver apenas Atividades (múltiplas)
https://geofront-frontend.onrender.com/index-refactored-ro.html?processo=PROC-2024-002&context=atividades

# Ver apenas Atividades (uma por vez)
https://geofront-frontend.onrender.com/index-refactored-ro.html?processo=PROC-2024-002&context=atividades&activityMode=single

# Ver tudo (default)
https://geofront-frontend.onrender.com/index-refactored-ro.html?processo=PROC-2024-002

Comportamento Esperado:
✅ context=imovel: Sidebar mostra APENAS seção Imóvel expandida
✅ context=empreendimento: Sidebar mostra APENAS seção Empreendimento expandida
✅ context=atividades: Sidebar mostra APENAS seção Atividades expandida
✅ activityMode=single: Ao clicar em "Ver" de uma atividade, outras atividades são automaticamente ocultadas
✅ activityMode=multiple: Múltiplas atividades podem ser visíveis simultaneamente (padrão)

No caso, as urls tem processo=PROC-2024-002, nesse caso, conforme o contexto que voçê for aplicar deve trocar para o valor correspondente. Exemplo, se estou no processo 42324556  colocar na url processo=42324556 . Esse será o campo para id dos shapes ou grupo de shapes. Ficou o nome "processo" mas o conteúdo é o que for pertinente.