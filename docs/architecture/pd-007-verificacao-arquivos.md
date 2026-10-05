# PD-007 — Limites aprovados e proposta de verificação

Data: 01/10/2026. Status: limites aprovados; solução técnica PROPOSTA, aguardando decisão. Não autoriza implementação.

## Decisões explícitas
- 26.214.400 bytes (25 MiB) por arquivo, inclusive ata PDF.
- Uma ata e até 10 anexos por versão: até 11 arquivos. Máximo aritmético 288.358.400 bytes (275 MiB); não representa quota global de armazenamento ou limite acumulado do histórico.
- Avast existente no host cliente; não há integração comprovada que ateste a verificação no servidor.
- Usuário autorizou avaliar e propor solução no servidor Docker/WSL, não aprovou ainda uma tecnologia.

## Proposta para decisão
Usar ClamAV em contêiner próprio no servidor, com clamd e atualização de assinaturas via FreshClam. A documentação oficial oferece imagem Docker e protocolo INSTREAM. Compatibilidade operacional com o host específico ainda não foi testada. Licença GPLv2; revisar obrigações de distribuição antes de empacotar/distribuir o produto.

Fluxo proposto: upload para área privada de quarentena; validação de tamanho, formato/conteúdo, macros e PDF sem senha conforme RN-015; envio dos bytes ao scanner; liberação somente após validações aprovadas e exame completo sem detecção. Detecção rejeita o arquivo. Erro, timeout, exame incompleto ou limite interno atingido não equivalem a arquivo limpo: manter indisponível para publicação/download e informar pendência de verificação. Arquivos previamente aceitos continuam sob as regras existentes.

Manter scanner em rede interna sem porta pública; varredura local sem enviar documentos a serviço externo. FreshClam precisa de acesso aos servidores de atualização. Persistir assinaturas em volume; fixar versão/imagem e digest após pesquisa PD-011. Dimensionar cerca de 4 GiB para o scanner conforme recomendação Docker oficial, além da aplicação e banco; capacidade real será medida antes da implantação.

Configurar StreamMaxLength para comportar 26.214.400 bytes, sem confundir limite de upload com limites de extração interna dos contêineres Office/ODF. Definir e testar MaxFileSize, MaxScanSize, profundidade, quantidade de itens extraídos e tratamento de limites de inspeção. Não concluir que resposta sem detecção comprova ausência de malware; validação de formato permanece independente.

Alternativas: produto comercial com integração Linux/API documentada (custo e licença a avaliar); serviço remoto (exigiria decisão de transferência de documentos). Recomendação: ClamAV local por suporte Docker documentado e integração de varredura sem remessa externa de documentos.

## Pendências
Aprovação da solução e comportamento em indisponibilidade; recursos disponíveis no servidor; parâmetros técnicos de timeout, retentativa, atualização/defasagem das assinaturas e extração para contrato TASK-001/011; capacidade total de armazenamento antes da produção, sem presumir que 275 MiB limita todo o histórico.

## Fontes oficiais consultadas
- https://docs.clamav.net/manual/Installing/Docker.html — imagem, persistência, isolamento e dimensionamento.
- https://docs.clamav.net/manual/Usage/ClamdProtocol.html — INSTREAM e StreamMaxLength.
- https://docs.clamav.net/manual/Usage/Scanning.html — uso do scanner e limites.
- https://docs.clamav.net/ — componentes e licença GPLv2.

## Validação planejada, não executada
Arquivos limpos, amostra de teste antimalware apropriada, formatos inválidos, macros, PDF protegido, 25 MiB exatos e +1 byte, 10 e 11 anexos, scanner indisponível, timeout e limites de extração. Gate real em TASK-011; nenhuma instalação ou teste realizado nesta análise.
