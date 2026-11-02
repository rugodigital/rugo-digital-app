"use client";

import { useState } from "react";

const initialClients = [
  {
    id: 1,
    name: "Sunrise Landscaping",
    industry: "Landscaping",
    location: "Suffolk County, NY",
    services: ["Lead Generation", "Social Media"],
    status: "Active"
  },
  {
    id: 2,
    name: "Premier Home Renovations",
    industry: "Home Improvement",
    location: "Long Island, NY",
    services: ["Google Ads", "Lead Generation"],
    status: "Active"
  },
  {
    id: 3,
    name: "Coastal Cleaning Co.",
    industry: "Cleaning",
    location: "Patchogue, NY",
    services: ["Social Media"],
    status: "Planning"
  }
];

const initialLeads = [
  { id: 1, clientId: 1, name: "Demo Lead 001", status: "New" },
  { id: 2, clientId: 1, name: "Demo Lead 002", status: "Contacted" },
  { id: 3, clientId: 2, name: "Demo Lead 003", status: "New" }
];

export default function Home() {
  const [clients, setClients] = useState(initialClients);
  const [leads, setLeads] = useState(initialLeads);
  const [selected, setSelected] = useState(null);
  const [tab, setTab] = useState("Dashboard");
  const [messages, setMessages] = useState([]);
  const [notice, setNotice] = useState("");

  const selectedClient = clients.find(c => c.id === selected);

  function generateLeads() {
    const client = selectedClient || clients[0];
    const newLeads = Array.from({ length: 3 }, (_, i) => ({
      id: Date.now() + i,
      clientId: client.id,
      name: `Demo Lead ${String(leads.length + i + 1).padStart(3, "0")}`,
      status: "New"
    }));
    setLeads(previous => [...previous, ...newLeads]);
    setNotice("3 fictional test leads generated. No real contacts were accessed.");
  }

  function draftMessage() {
    const client = selectedClient || clients[0];
    setMessages(previous => [
      ...previous,
      {
        id: Date.now(),
        clientId: client.id,
        text: `Hello! We're reaching out on behalf of ${client.name}. Would you be interested in learning more about our services?`,
        status: "Pending"
      }
    ]);
    setNotice("Demo message drafted. Nothing has been sent.");
  }

  const panel = {
    background: "#182337",
    border: "1px solid #2c3c55",
    borderRadius: 14,
    padding: 20,
    marginBottom: 16
  };

  const button = {
    background: "#28c6ae",
    color: "#07131d",
    border: 0,
    borderRadius: 9,
    padding: "11px 15px",
    fontWeight: 700,
    cursor: "pointer",
    margin: "5px 6px 5px 0"
  };

  return (
    <main style={{
      minHeight: "100vh",
      background: "#0b1423",
      color: "#f5f7fa",
      fontFamily: "Arial, sans-serif",
      padding: 20
    }}>
      <div style={{ maxWidth: 1050, margin: "auto" }}>
        <header style={{ marginBottom: 25 }}>
          <h1>RUGO DIGITAL</h1>
          <p style={{ color: "#28c6ae" }}>
            Marketing Management Dashboard
          </p>
          <p>TEST MODE — No real messages or lead searches</p>
        </header>

        <nav style={{ marginBottom: 25 }}>
          {["Dashboard", "Clients", "Leads", "Messages"].map(item => (
            <button
              key={item}
              style={{
                ...button,
                background: tab === item ? "#28c6ae" : "#263750",
                color: tab === item ? "#07131d" : "white"
              }}
              onClick={() => setTab(item)}
            >
              {item}
            </button>
          ))}
        </nav>

        {notice && <div style={panel}>{notice}</div>}

        {tab === "Dashboard" && (
          <>
            <h2>Overview</h2>
            <div style={panel}>
              <h3>Total Clients: {clients.length}</h3>
              <h3>Demo Leads: {leads.length}</h3>
              <h3>Draft Messages: {messages.length}</h3>
              <h3>Active Campaigns: {
                clients.filter(c => c.status === "Active").length
              }</h3>
            </div>
            <button style={button} onClick={generateLeads}>
              Generate Test Leads
            </button>
            <button style={button} onClick={draftMessage}>
              Create Demo Message
            </button>
          </>
        )}

        {tab === "Clients" && (
          <>
            <h2>My Clients</h2>
            {clients.map(client => (
              <div key={client.id} style={panel}>
                <h3>{client.name}</h3>
                <p>{client.industry} — {client.location}</p>
                <p>Status: {client.status}</p>
                <button
                  style={button}
                  onClick={() => setSelected(
                    selected === client.id ? null : client.id
                  )}
                >
                  View Client
                </button>
                {selected === client.id && (
                  <div>
                    <h4>Current Services</h4>
                    <p>{client.services.join(", ")}</p>
                    <h4>Demo Leads</h4>
                    <p>{leads.filter(l => l.clientId === client.id).length}</p>
                    <button style={button} onClick={generateLeads}>
                      Generate Test Leads
                    </button>
                    <button style={button} onClick={draftMessage}>
                      Draft Message
                    </button>
                  </div>
                )}
              </div>
            ))}
          </>
        )}

        {tab === "Leads" && (
          <>
            <h2>Lead Tracker</h2>
            {leads.map(lead => (
              <div key={lead.id} style={panel}>
                <strong>{lead.name}</strong>
                <p>Client: {
                  clients.find(c => c.id === lead.clientId)?.name
                }</p>
                <label>Status: </label>
                <select
                  value={lead.status}
                  onChange={e => setLeads(previous =>
                    previous.map(l => l.id === lead.id
                      ? { ...l, status: e.target.value }
                      : l
                    )
                  )}
                >
                  <option>New</option>
                  <option>Contacted</option>
                  <option>Qualified</option>
                  <option>Closed</option>
                </select>
              </div>
            ))}
          </>
        )}

        {tab === "Messages" && (
          <>
            <h2>Message Approvals</h2>
            <button style={button} onClick={draftMessage}>
              Generate Draft
            </button>
            {messages.map(message => (
              <div key={message.id} style={panel}>
                <textarea
                  style={{ width: "100%", minHeight: 85 }}
                  value={message.text}
                  onChange={e => setMessages(previous =>
                    previous.map(m => m.id === message.id
                      ? { ...m, text: e.target.value }
                      : m
                    )
                  )}
                />
                <p>Status: {message.status}</p>
                <button
                  style={button}
                  onClick={() => setMessages(previous =>
                    previous.map(m => m.id === message.id
                      ? { ...m, status: "Approved (Simulation)" }
                      : m
                    )
                  )}
                >
                  Approve (Test Only)
                </button>
                <button
                  style={button}
                  onClick={() => setMessages(previous =>
                    previous.map(m => m.id === message.id
                      ? { ...m, status: "Rejected" }
                      : m
                    )
                  )}
                >
                  Reject
                </button>
              </div>
            ))}
          </>
        )}

        <footer style={{ marginTop: 40, color: "#8899aa" }}>
          Rugo Digital — Private Demo Prototype
        </footer>
      </div>
    </main>
  );
}
