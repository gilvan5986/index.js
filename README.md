const express = require('express');
const axios = require('axios');
const cors = require('cors');
require('dotenv').config();

const app = express();
app.use(cors());

const API_KEY = process.env.TE_API_KEY;
const BASE_URL = 'https://api.tradingeconomics.com/calendar';

app.get('/calendario', async (req, res) => {
  try {
    const response = await axios.get(BASE_URL, {
      params: {
        c: API_KEY,
        f: 'json'
      }
    });
    res.json(response.data);
  } catch (error) {
    res.status(500).json({ error: 'Erro ao buscar dados' });
  }
});

const PORT = process.env.PORT || 3000;
app.listen(PORT, () => console.log(`Servidor rodando na porta ${PORT}`));
