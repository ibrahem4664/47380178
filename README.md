# import React from "react";
import { BrowserRouter as Router, Route, Routes, Link } from "react-router-dom";
import { Card, CardContent } from "@/components/ui/card";
import { Button } from "@/components/ui/button";
import { Input } from "@/components/ui/input";
import { Textarea } from "@/components/ui/textarea";
import { useState } from "react";

function HomePage() {
  return (
    <div className="p-6">
      <h1 className="text-2xl font-bold">أخبار المجمع الطبي</h1>
      <Card className="mt-4 p-4">
        <CardContent>
          <p>فرص عمل جديدة للأطباء والممرضين في مستشفيات مصر</p>
          <Button className="mt-2">تصفح الفرص</Button>
        </CardContent>
      </Card>
    </div>
  );
}

function LoginPage() {
  return (
    <div className="p-6 flex flex-col items-center">
      <h2 className="text-xl font-bold">تسجيل الدخول</h2>
      <Input placeholder="البريد الإلكتروني" className="mt-4" />
      <Input type="password" placeholder="كلمة المرور" className="mt-2" />
      <Button className="mt-4">تسجيل الدخول</Button>
    </div>
  );
}

function ChatPage() {
  const [message, setMessage] = useState("");
  const [messages, setMessages] = useState([]);

  const sendMessage = () => {
    if (message.trim()) {
      setMessages([...messages, message]);
      setMessage("");
    }
  };

  return (
    <div className="p-6">
      <h2 className="text-xl font-bold">الدردشة</h2>
      <div className="mt-4 border p-4 rounded">
        {messages.map((msg, index) => (
          <p key={index} className="mb-2 p-2 bg-gray-100 rounded">{msg}</p>
        ))}
      </div>
      <Textarea
        className="mt-4"
        placeholder="اكتب رسالتك..."
        value={message}
        onChange={(e) => setMessage(e.target.value)}
      />
      <Button className="mt-2" onClick={sendMessage}>إرسال</Button>
    </div>
  );
}

function App() {
  return (
    <Router>
      <div className="p-6 flex flex-col items-center">
        <nav className="mb-6">
          <Link to="/" className="mr-4">الرئيسية</Link>
          <Link to="/login" className="mr-4">تسجيل الدخول</Link>
          <Link to="/chat">الدردشة</Link>
        </nav>
        <Routes>
          <Route path="/" element={<HomePage />} />
          <Route path="/login" element={<LoginPage />} />
          <Route path="/chat" element={<ChatPage />} />
        </Routes>
      </div>
    </Router>
  );
}

export default App;

