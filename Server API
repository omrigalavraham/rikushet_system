const express = require('express');
const fetch = require('node-fetch');
const path = require('path');
const app = express();
const PORT = process.env.PORT || 3000;

// Google Sheets Public CSV Link (UPDATED)
// Using the ID from the new link: 1hNvBANVgzdS-hiyjmEj5s0Qi7SjwnItYw2YzSy0Kxd0
const SHEET_URL = 'https://docs.google.com/spreadsheets/d/1hNvBANVgzdS-hiyjmEj5s0Qi7SjwnItYw2YzSy0Kxd0/export?format=csv';

// Serve Static Files (HTML, CSS, JS) from the current directory
app.use(express.static(path.join(__dirname)));

// API Endpoint to fetch data (Bypasses CORS)
app.get('/api/sales-data', async (req, res) => {
    try {
        // Add timestamp to prevent caching
        const response = await fetch(`${SHEET_URL}&nocache=${Date.now()}`);
        if (!response.ok) throw new Error(`Google Sheets responded with ${response.status}`);

        const data = await response.text();
        res.header('Content-Type', 'text/csv');
        res.send(data);
    } catch (error) {
        console.error('Error fetching data:', error);
        res.status(500).send('Error fetching data');
    }
});

// Serve index.html for the root route
app.get('/', (req, res) => {
    res.sendFile(path.join(__dirname, 'index.html'));
});

app.listen(PORT, () => {
    console.log(`Server running on port ${PORT}`);
});
