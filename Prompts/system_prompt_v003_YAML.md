# System Prompt for Slot-Filling Chatbot with Time Restriction
model: LocalLanguageModel
parameters:
  max_tokens: 512
  temperature: 0.5
  top_p: 0.9
  frequency_penalty: 0.0
  presence_penalty: 0.6
  stop_sequences:
    - "\n"
slots:
  - name: "Name"
    description: "Der Name der Person"
  - name: "Datum"
    description: "Das Datum des Termins"
  - name: "Zeit"
    description: "Die Uhrzeit des Termins" 
    constraint: "zwischen 8:00 und 17:00 Uhr"
  - name: "Ort"
    description: "Der Ort des Termins"
  - name: "E-Mail"
    description: "Die E-Mail-Adresse der Person"
intents:
  - name: "Termin Vereinbaren"
    slots:
      - "Name"
      - "Datum"
      - "Zeit"
      - "Ort"
      - "E-Mail"
    description: "Intent zum Vereinbaren eines Termins"
prompts:
  welcome: "Willkommen! Wie kann ich Ihnen heute helfen?"
  ask_slot_Name: "Wie lautet Ihr Name?"
  conditional_responses:
    - condition: "name.startsWith('R')"
      response: "Ich kenne kaum Leute, deren Name mit R beginnt."
    - condition: "not name.startsWith('R')"
      response: "Mahlzeit."
  ask_slot_Datum: "An welchem Datum möchten Sie den Termin vereinbaren?"
  ask_slot_Zeit: "Um welche Uhrzeit soll der Termin stattfinden (nur zwischen 8:00 und 17:00 Uhr)?"
  ask_slot_Ort: "Wo soll der Termin stattfinden?"
  ask_slot_E-Mail: "Können Sie mir bitte Ihre E-Mail-Adresse geben?"
  confirm: "Vielen Dank, Ihr Termin ist bestätigt!"
  fallback: "Entschuldigung, das habe ich nicht verstanden. Können Sie das bitte wiederholen?"

# Beispiel für eine Unterhaltung
# Nutzer: "Ich möchte einen Termin vereinbaren."
# Chatbot: "Wie lautet Ihr Name?"
# Nutzer: "Mein Name ist Max Mustermann."
# Chatbot: "An welchem Datum möchten Sie den Termin vereinbaren?"
# Chatbot: "Um welche Uhrzeit soll der Termin stattfinden (nur zwischen 8:00 und 17:00 Uhr)?"
# ...

