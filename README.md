
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>WB Reformas - Simulador de Orçamento</title>
    <style>
        :root {
            --cor-primaria: #d97706; /* Amarelo/Dourado WB */
            --cor-fundo: #0a0a0c;
            --cor-card: #141419;
            --cor-borda: #2a2a35;
            --cor-texto: #f1f5f9;
            --cor-sucesso: #25D366;
        }

        * { margin: 0; padding: 0; box-sizing: border-box; font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; }
        body { background-color: var(--cor-fundo); color: var(--cor-texto); padding-bottom: 50px; }

        header {
            background: linear-gradient(180deg, #1f1402 0%, #0a0a0c 100%);
            border-bottom: 3px solid var(--cor-primaria);
            padding: 30px 20px;
            text-align: center;
        }
        header h1 { font-size: 2rem; font-weight: 900; letter-spacing: 2px; text-transform: uppercase; color: #fff; }
        header h1 span { color: var(--cor-primaria); }
        header p { color: #cbd5e1; font-size: 0.9rem; margin-top: 5px; }
        .contato-topo { color: var(--cor-primaria); font-size: 0.85rem; font-weight: bold; margin-top: 6px; }

        .container { max-width: 600px; margin: 20px auto; padding: 0 15px; }

        .card {
            background: var(--cor-card);
            border: 1px solid var(--cor-borda);
            border-radius: 12px;
            padding: 22px;
            margin-bottom: 20px;
            box-shadow: 0 8px 25px rgba(0,0,0,0.6);
        }
        .card h2 {
            color: var(--cor-primaria);
            font-size: 1.15rem;
            margin-bottom: 18px;
            text-transform: uppercase;
            border-bottom: 1px solid var(--cor-borda);
            padding-bottom: 10px;
        }

        .form-group { margin-bottom: 15px; }
        .form-group label { display: block; font-size: 0.85rem; color: #94a3b8; margin-bottom: 6px; font-weight: bold; }
        select, input {
            width: 100%;
            padding: 13px;
            border-radius: 8px;
            background: #0a0a0c;
            border: 1px solid var(--cor-borda);
            color: #fff;
            font-size: 1rem;
            outline: none;
        }
        select:focus, input:focus { border-color: var(--cor-primaria); }

        /* CHECKBOXES DE ADICIONAIS */
        .opcional-item {
            display: flex;
            align-items: center;
            justify-content: space-between;
            background: #0d0d12;
            border: 1px solid var(--cor-borda);
            padding: 12px 15px;
            border-radius: 8px;
            margin-bottom: 8px;
            cursor: pointer;
        }
        .opcional-item input { width: 20px; height: 20px; accent-color: var(--cor-primaria); cursor: pointer; }
        .opcional-info { flex: 1; margin-left: 12px; font-size: 0.9rem; }
        .opcional-preco { font-weight: bold; color: var(--cor-primaria); font-size: 0.9rem; }

        .resumo-total {
            background: linear-gradient(145deg, #1a150b, #0a0a0c);
            border: 2px solid var(--cor-primaria);
            border-radius: 10px;
            padding: 18px;
            text-align: center;
            margin-top: 15px;
        }
        .resumo-total span { font-size: 0.85rem; color: #cbd5e1; }
        .valor-gigante { font-size: 2.2rem; font-weight: 900; color: var(--cor-primaria); margin: 5px 0; }
        .aviso-regra { font-size: 0.75rem; color: #94a3b8; margin-top: 8px; line-height: 1.4; }
        .aviso-parcelamento { font-size: 0.85rem; color: #25D366; font-weight: bold; margin-top: 8px; }

        .btn-zap {
            width: 100%;
            padding: 16px;
            background: var(--cor-sucesso);
            color: #000;
            border: none;
            border-radius: 8px;
            font-weight: 900;
            font-size: 1.05rem;
            text-transform: uppercase;
            cursor: pointer;
            margin-top: 15px;
            display: flex;
            justify-content: center;
            align-items: center;
            gap: 8px;
        }
    </style>
</head>
<body>

    <header>
        <h1>WB <span>REFORMAS</span></h1>
        <p>Pintura • Elétrica • Drywall • Alvenaria e Acabamento</p>
        <div class="contato-topo">📲 Atendimento WhatsApp: (11) 97661-5787</div>
    </header>

    <div class="container">
        
        <div class="card">
            <h2>🛠 Simulador de Projeto</h2>
            
            <div class="form-group">
                <label>1. Escolha o Serviço Principal / Base</label>
                <select id="servicoBase" onchange="calcularOrcamento()">
                    <option value="2900|Reforma de Banheiro Completa">Reforma de Banheiro (Base Mão de Obra) - R$ 2.900</option>
                    <option value="4500|Reforma de Cozinha Completa">Reforma de Cozinha (Base Mão de Obra) - R$ 4.500</option>
                    <option value="1500|Pintura e Acabamento por Cômodo">Pintura e Acabamento por Cômodo - R$ 1.500</option>
                </select>
            </div>

            <div class="form-group">
                <label>2. Sua Região / Bairro</label>
                <select id="regiaoAtendimento">
                    <option value="São Paulo - Centro / Zona Sul">São Paulo - Centro / Zona Sul</option>
                    <option value="São Paulo - Zona Leste / Norte">São Paulo - Zona Leste / Norte</option>
                    <option value="São Paulo - Zona Oeste / Osasco">São Paulo - Zona Oeste / Osasco</option>
                    <option value="Grande SP / ABC Paulista">Grande SP / ABC Paulista</option>
                </select>
            </div>

            <label style="display:block; font-size:0.85rem; color:#94a3b8; margin-bottom:8px; font-weight:bold;">3. Detalhes e Acabamentos Especiais (Opcionais)</label>
            
            <label class="opcional-item">
                <input type="checkbox" value="Nicho Embutido no Box|350" onchange="calcularOrcamento()">
                <div class="opcional-info">Nicho Embutido na Alvenaria / Box</div>
                <div class="opcional-preco">+ R$ 350,00</div>
            </label>

            <label class="opcional-item">
                <input type="checkbox" value="Corte Meia-Esquadria 45° nos Cantos|450" onchange="calcularOrcamento()">
                <div class="opcional-info">Acabamento 45 Graus (Meia-Esquadria)</div>
                <div class="opcional-preco">+ R$ 450,00</div>
            </label>

            <label class="opcional-item">
                <input type="checkbox" value="Instalação / Adequação Elétrica|600" onchange="calcularOrcamento()">
                <div class="opcional-info">Pontos Novos de Elétrica e Iluminação</div>
                <div class="opcional-preco">+ R$ 600,00</div>
            </label>

            <label class="opcional-item">
                <input type="checkbox" value="Instalação de Louças e Metais (Vaso/Cuba)|250" onchange="calcularOrcamento()">
                <div class="opcional-info">Instalação de Vaso, Cuba e Metais</div>
                <div class="opcional-preco">+ R$ 250,00</div>
            </label>
        </div>

        <div class="card">
            <h2>💳 Forma de Pagamento Preferida</h2>
            <div class="form-group" style="margin-bottom:0;">
                <label>Como pretende realizar o acerto?</label>
                <select id="formaPagamento">
                    <option value="Cartão de Crédito (Parcelado)">Cartão de Crédito (Parcelado)</option>
                    <option value="Cartão de Débito">Cartão de Débito</option>
                    <option value="Dinheiro / Pix à Vista">Dinheiro / Pix à Vista</option>
                </select>
            </div>
        </div>

        <div class="card">
            <h2>📋 Resumo do Orçamento</h2>
            
            <div class="form-group">
                <label>Seu Nome</label>
                <input type="text" id="nomeCliente" placeholder="Digite seu nome...">
            </div>

            <div class="resumo-total">
                <span>Estimativa Inicial de Mão de Obra:</span>
                <div class="valor-gigante" id="valorTotalDisplay">R$ 2.900,00</div>
                <div id="infoParcelamento" class="aviso-parcelamento"></div>
                <div class="aviso-regra">⚠️ <em>Valores iniciais de referência. O orçamento final detalhado de materiais e execução é confirmado após a visita técnica no local.</em></div>
            </div>

            <button class="btn-zap" onclick="enviarOrcamentoZap()">
                📲 Enviar Detalhes para o WhatsApp da WB
            </button>
        </div>
    </div>

    <script>
        const WHATSAPP_WB = "5511976615787"; 

        function calcularOrcamento() {
            const servicoParts = document.getElementById('servicoBase').value.split('|');
            let total = parseFloat(servicoParts[0]);

            const checkboxes = document.querySelectorAll('.opcional-item input[type="checkbox"]:checked');
            checkboxes.forEach(cb => {
                const precoOpcional = parseFloat(cb.value.split('|')[1]);
                total += precoOpcional;
            });

            document.getElementById('valorTotalDisplay').innerText = `R$ ${total.toFixed(2).replace('.', ',')}`;

            const infoParc = document.getElementById('infoParcelamento');
            if (total > 10000) {
                const valorParcela = (total / 5).toFixed(2).replace('.', ',');
                infoParc.innerHTML = `✨ Condição Especial: Acima de R$ 10.000 em até <strong>5x sem juros</strong> de R$ ${valorParcela} no cartão!`;
            } else {
                infoParc.innerHTML = `💳 Parcelamento disponível no cartão (consulte condições).`;
            }
        }

        function enviarOrcamentoZap() {
            const nome = document.getElementById('nomeCliente').value.trim() || "Cliente";
            const servicoParts = document.getElementById('servicoBase').value.split('|');
            const nomeServico = servicoParts[1];
            const regiao = document.getElementById('regiaoAtendimento').value;
            const pagamento = document.getElementById('formaPagamento').value;

            let total = parseFloat(servicoParts[0]);
            let msg = `🔥 *ORÇAMENTO DE REFORMA - WB* 🔥\n\n`;
            msg += `👤 *Cliente:* ${nome}\n`;
            msg += `📍 *Região:* ${regiao}\n\n`;
            msg += `🛠 *Serviço Principal:* ${nomeServico} (R$ ${total.toFixed(2)})\n`;

            const checkboxes = document.querySelectorAll('.opcional-item input[type="checkbox"]:checked');
            if (checkboxes.length > 0) {
                msg += `\n➕ *Adicionais Escolhidos:*\n`;
                checkboxes.forEach(cb => {
                    const dados = cb.value.split('|');
                    total += parseFloat(dados[1]);
                    msg += `▪ ${dados[0]} (+R$ ${parseFloat(dados[1]).toFixed(2)})\n`;
                });
            }

            msg += `\n💳 *Pagamento Desejado:* ${pagamento}\n`;
            msg += `💰 *Estimativa Total:* R$ ${total.toFixed(2).replace('.', ',')}\n`;
            if (total > 10000) {
                msg += `*(Elegível para até 5x sem juros)*\n`;
            }
            msg += `*(Cliente ciente de que valores exatos dependem de vistoria técnica)*\n\n`;
            msg += `Olá WB Reformas! Simulei meu projeto no site de vocês e gostaria de agendar uma visita técnica.`;

            window.open(`https://wa.me/${WHATSAPP_WB}?text=${encodeURIComponent(msg)}`, '_blank');
        }

        calcularOrcamento();
    </script>
</body>
</html>
