// File: src/components/CryptoChart.tsx import React, { useEffect, useState } from "react"; import { LineChart, Line, XAxis, YAxis, CartesianGrid, Tooltip, ResponsiveContainer, } from "recharts";

interface ChartData { time: string; price: number; }

interface Props { coinId: string; // e.g., 'ethereum', 'bitcoin' title?: string; }

export default function CryptoChart({ coinId, title }: Props) { const [data, setData] = useState<ChartData[]>([]);

useEffect(() => { const fetchData = async () => { const now = Math.floor(Date.now() / 1000); const from = now - 3600 * 24; // 24 hours ago const res = await fetch( https://api.coingecko.com/api/v3/coins/${coinId}/market_chart/range?vs_currency=usd&from=${from}&to=${now} ); const json = await res.json(); const chartData = json.prices.map((d: number[]) => ({ time: new Date(d[0]).toLocaleTimeString([], { hour: "2-digit", minute: "2-digit" }), price: d[1], })); setData(chartData); }; fetchData(); }, [coinId]);

return ( <div className="w-full p-4"> {title && <h2 className="text-xl font-semibold mb-2 text-center">{title}</h2>} <div className="w-full h-64"> <ResponsiveContainer width="100%" height="100%"> <LineChart data={data} margin={{ top: 10, right: 20, left: 0, bottom: 0 }}> <CartesianGrid strokeDasharray="3 3" /> <XAxis dataKey="time" hide /> <YAxis domain={["auto", "auto"]} /> <Tooltip /> <Line type="monotone" dataKey="price" stroke="#8884d8" strokeWidth={2} dot={false} /> </LineChart> </ResponsiveContainer> </div> </div> ); }

