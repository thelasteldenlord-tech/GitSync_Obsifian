```js
import React, { useState } from 'react';
import { Card, CardContent, CardHeader, CardTitle } from "@/components/ui/card"
import { Select, SelectContent, SelectItem, SelectTrigger, SelectValue } from "@/components/ui/select"
import { LineChart, Line, XAxis, YAxis, CartesianGrid, Tooltip, Legend, ResponsiveContainer } from 'recharts';

const generateData = (campaign) => {
  const baseCTR = campaign === 'Email' ? 0.05 : campaign === 'Social Media' ? 0.03 : 0.02;
  const baseConversionRate = campaign === 'Email' ? 0.1 : campaign === 'Social Media' ? 0.05 : 0.03;
  
  return [
    { name: 'Week 1', Impressions: Math.floor(Math.random() * 10000) + 5000, Clicks: Math.floor(Math.random() * 1000) + 100, Conversions: Math.floor(Math.random() * 100) + 10 },
    { name: 'Week 2', Impressions: Math.floor(Math.random() * 10000) + 5000, Clicks: Math.floor(Math.random() * 1000) + 100, Conversions: Math.floor(Math.random() * 100) + 10 },
    { name: 'Week 3', Impressions: Math.floor(Math.random() * 10000) + 5000, Clicks: Math.floor(Math.random() * 1000) + 100, Conversions: Math.floor(Math.random() * 100) + 10 },
    { name: 'Week 4', Impressions: Math.floor(Math.random() * 10000) + 5000, Clicks: Math.floor(Math.random() * 1000) + 100, Conversions: Math.floor(Math.random() * 100) + 10 },
  ].map(week => ({
    ...week,
    CTR: ((week.Clicks / week.Impressions) * (1 + Math.random() * 0.4 - 0.2) + baseCTR).toFixed(4),
    'Conversion Rate': ((week.Conversions / week.Clicks) * (1 + Math.random() * 0.4 - 0.2) + baseConversionRate).toFixed(4)
  }));
};

const calculateDifference = (value1, value2) => {
  const diff = ((value1 - value2) / value2 * 100).toFixed(1);
  return { 
    value: `${diff > 0 ? '+' : ''}${diff}%`,
    class: diff > 0 ? 'text-green-500' : diff < 0 ? 'text-red-500' : 'text-gray-500'
  };
};

const MetricCard = ({ title, value1, value2, campaign1, campaign2 }) => {
  const diff = value2 !== undefined ? calculateDifference(value1, value2) : null;
  
  return (
    <Card className="flex flex-col justify-between h-full bg-gray-900 text-white">
      <CardHeader>
        <CardTitle className="text-sm font-medium text-gray-400">{title}</CardTitle>
      </CardHeader>
      <CardContent>
        <div className="space-y-2">
          <div className="text-2xl font-bold">{value1.toLocaleString()}</div>
          {diff && (
            <div className="text-sm">
              <span className="text-gray-400">vs {campaign2}: </span>
              <span className={diff.class}>{diff.value}</span>
            </div>
          )}
        </div>
      </CardContent>
    </Card>
  );
};

const PerformanceChart = ({ data1, data2, campaign1, campaign2 }) => (
  <ResponsiveContainer width="100%" height={400}>
    <LineChart>
      <CartesianGrid strokeDasharray="3 3" stroke="#374151" />
      <XAxis dataKey="name" stroke="#9CA3AF" />
      <YAxis yAxisId="left" stroke="#9CA3AF" />
      <YAxis yAxisId="right" orientation="right" stroke="#9CA3AF" />
      <Tooltip contentStyle={{ backgroundColor: '#1F2937', border: 'none' }} />
      <Legend />
      {[
        { data: data1, suffix: ` (${campaign1})`, colors: ['#8B5CF6', '#10B981', '#F59E0B'] },
        { data: data2, suffix: ` (${campaign2})`, colors: ['#6366F1', '#059669', '#D97706'] }
      ].map(({ data, suffix, colors }) => data && [
        <Line yAxisId="left" type="monotone" dataKey="Impressions" data={data} name={`Impressions${suffix}`} stroke={colors[0]} dot={false} />,
        <Line yAxisId="left" type="monotone" dataKey="Clicks" data={data} name={`Clicks${suffix}`} stroke={colors[1]} dot={false} />,
        <Line yAxisId="right" type="monotone" dataKey="Conversions" data={data} name={`Conversions${suffix}`} stroke={colors[2]} dot={false} />
      ])}
    </LineChart>
  </ResponsiveContainer>
);

const MarketingDashboard = () => {
  const [campaign1, setCampaign1] = useState('Email');
  const [campaign2, setCampaign2] = useState('Social Media');
  
  const data1 = generateData(campaign1);
  const data2 = generateData(campaign2);

  const calculateMetrics = (data) => ({
    impressions: data.reduce((sum, week) => sum + week.Impressions, 0),
    clicks: data.reduce((sum, week) => sum + week.Clicks, 0),
    conversions: data.reduce((sum, week) => sum + week.Conversions, 0)
  });

  const metrics1 = calculateMetrics(data1);
  const metrics2 = calculateMetrics(data2);

  return (
    <div className="p-4 space-y-6 bg-gray-950 text-white min-h-screen">
      <h1 className="text-3xl font-bold">Campaign Comparison Dashboard</h1>
      
      <div className="grid grid-cols-2 gap-4">
        <Select onValueChange={setCampaign1} defaultValue={campaign1}>
          <SelectTrigger className="bg-gray-900 text-white border-gray-700">
            <SelectValue placeholder="Select primary campaign" />
          </SelectTrigger>
          <SelectContent className="bg-gray-900 text-white border-gray-700">
            <SelectItem value="Email">Email</SelectItem>
            <SelectItem value="Social Media">Social Media</SelectItem>
            <SelectItem value="Display Ads">Display Ads</SelectItem>
          </SelectContent>
        </Select>

        <Select onValueChange={setCampaign2} defaultValue={campaign2}>
          <SelectTrigger className="bg-gray-900 text-white border-gray-700">
            <SelectValue placeholder="Select comparison campaign" />
          </SelectTrigger>
          <SelectContent className="bg-gray-900 text-white border-gray-700">
            <SelectItem value="Email">Email</SelectItem>
            <SelectItem value="Social Media">Social Media</SelectItem>
            <SelectItem value="Display Ads">Display Ads</SelectItem>
          </SelectContent>
        </Select>
      </div>

      <div className="grid grid-cols-1 md:grid-cols-3 gap-4">
        <MetricCard 
          title="Total Impressions" 
          value1={metrics1.impressions}
          value2={metrics2.impressions}
          campaign1={campaign1}
          campaign2={campaign2}
        />
        <MetricCard 
          title="Total Clicks" 
          value1={metrics1.clicks}
          value2={metrics2.clicks}
          campaign1={campaign1}
          campaign2={campaign2}
        />
        <MetricCard 
          title="Total Conversions" 
          value1={metrics1.conversions}
          value2={metrics2.conversions}
          campaign1={campaign1}
          campaign2={campaign2}
        />
      </div>

      <Card className="bg-gray-900 text-white">
        <CardHeader>
          <CardTitle>Performance Comparison</CardTitle>
        </CardHeader>
        <CardContent>
          <PerformanceChart 
            data1={data1} 
            data2={data2}
            campaign1={campaign1}
            campaign2={campaign2}
          />
        </CardContent>
      </Card>
    </div>
  );
};

export default MarketingDashboard;