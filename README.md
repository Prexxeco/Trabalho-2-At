# Trabalho-2-At

    import React, { useState } from 'react';
    import { Presentation as GasStation, DollarSign, Droplets } from 'lucide-react';

    type FuelType = 'gasolina' | 'etanol' | 'diesel';
    type InputType = 'litros' | 'valor';

    interface FuelPrices {
      gasolina: number;
      etanol: number;
      diesel: number;
    }

    function App() {
      const [fuelType, setFuelType] = useState<FuelType>('gasolina');
      const [inputType, setInputType] = useState<InputType>('litros');
      [inputValue, setInputValue] = useState<string>('');
      const [isRefueling, setIsRefueling] = useState(false);
      const [receipt, setReceipt] = useState<{ liters: number; total: number } | null>(null);

      const fuelPrices: FuelPrices = {
    gasolina: 5.50,
    etanol: 3.80,
    diesel: 6.20
      };

      const calculateFuel = () => {
    const value = parseFloat(inputValue);
    if (isNaN(value) || value <= 0) return;

    const price = fuelPrices[fuelType];
    let liters: number;
    let total: number;

    if (inputType === 'litros') {
      liters = value;
      total = value * price;
    } else {
      liters = value / price;
      total = value;
    }

    setIsRefueling(true);
    
    // Simula o processo de abastecimento
    setTimeout(() => {
      setIsRefueling(false);
      setReceipt({ liters, total });
    }, 2000);
      };

      const resetTransaction = () => {
    setInputValue('');
    setReceipt(null);
      };

      return (
    <div className="min-h-screen bg-gradient-to-b from-blue-100 to-blue-200 p-8">
      <div className="max-w-md mx-auto bg-white rounded-xl shadow-lg p-6">
        <div className="flex items-center justify-center mb-6">
          <GasStation className="w-10 h-10 text-blue-600" />
          <h1 className="text-2xl font-bold ml-2 text-gray-800">Posto de Combustível</h1>
        </div>

        {!isRefueling && !receipt ? (
          <>
            <div className="mb-6">
              <label className="block text-sm font-medium text-gray-700 mb-2">Selecione o Combustível</label>
              <div className="grid grid-cols-3 gap-2">
                {Object.entries(fuelPrices).map(([type, price]) => (
                  <button
                    key={type}
                    onClick={() => setFuelType(type as FuelType)}
                    className={`p-2 rounded ${
                      fuelType === type
