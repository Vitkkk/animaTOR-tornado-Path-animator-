# animaTOR 🌪️
Protótipo de animação de trajetórias de tornados: KML → marcador em movimento, rastro progressivo e câmera seguindo. Interface em português, responsiva, sem dependências de frontend.

## Rodar no GitHub Codespaces / ambiente Work
Abra o repositório em um ambiente de desenvolvimento, execute `npm start` e abra a porta **3000**. Ou execute `python3 -m http.server 3000`. No Codespaces, a configuração de devcontainer inicia o servidor ao conectar.

## Publicar com GitHub Actions
Em **Settings → Pages → Build and deployment**, selecione **GitHub Actions**. Execute **Actions → Publicar animaTOR → Run workflow**. O workflow também executa em pushes à main. O endereço aparece no deployment do workflow; um workflow não é um servidor de prévia permanente.

## Usar
1. Comece com a demonstração fictícia ou importe seu `.kml`.
2. Selecione a trajetória e, se houver, o polígono correspondente na lista de áreas de danos.
3. Confira o sentido; use **Inverter** se necessário.
4. Ajuste cor, marcador, duração e câmera. Inicie ou arraste a linha do tempo.
5. Use **Gravar vídeo WebM** para gravar o canvas em tempo real. Mantenha a aba visível; o download começa ao terminar. Os controles HTML não entram no vídeo; título e créditos entram.

## Escopo e limitações
- Lê LineString, gx:Track e Polygon, inclusive em MultiGeometry e pastas. Anéis internos são preservados na máscara.
- Não lê KMZ, NetworkLink ou imagens de GroundOverlay; não busca arquivos externos do KML.
- Usa velocidade uniforme por distância projetada e duração definida pelo usuário; timestamps ainda não controlam a animação.
- Sem linha central: estima eixo por componentes principais e cortes transversais. Não é reconstrução do movimento real. Curvas fechadas, ramificações ou polígonos fragmentados exigem uma linha central fornecida pelo usuário.
- A faixa original é rasterizada em até 600 pixels no maior lado; revelação por posição mais próxima num eixo amostrado em 200 segmentos. Curvas que passam muito perto de si mesmas podem causar artefatos. A largura deriva do polígono, não do círculo.
- Marcador tem tamanho em pixels, não representa diâmetro físico. Distância exibida é aproximada.
- Mapas requerem rede; a grade funciona offline. Esri World Imagery e OpenStreetMap mantêm seus créditos. Uso dos mapas depende dos termos dos respectivos provedores; nenhuma imagem de Google Earth é incluída.
- Gravação depende de MediaRecorder, WebM e suporte CORS do provedor. Sem MP4, relevo 3D ou exportação determinística de alta resolução nesta versão.
- KML permanece no navegador. Dados importados são exibidos como texto, nunca interpretados como HTML.

## Validação
`npm run check` verifica sintaxe. O teste `tests/smoke.cjs` foi preparado para verificar importação, seleção, progresso, inversão, polígono isolado, XML inválido e gravação offline. A execução local do navegador foi bloqueada pela indisponibilidade do Chromium; o workflow executa esse teste no GitHub. A demonstração é inteiramente fictícia.
