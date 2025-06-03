<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Interactive Liver Failure Case Study Quiz</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        body {
            font-family: 'Inter', sans-serif;
        }
        .content-box {
            @apply bg-white p-6 rounded-lg shadow-md mb-6;
        }
        .question-title {
            @apply text-xl font-semibold mb-3 text-slate-700;
        }
        .section-title {
            @apply text-lg font-semibold mb-2 text-sky-700;
        }
        .data-table table {
            @apply w-full text-sm text-left text-gray-500;
        }
        .data-table th {
            @apply px-4 py-2 bg-sky-50 text-sky-700 font-semibold rounded-t-md;
        }
        .data-table td {
            @apply px-4 py-2 border-b border-gray-200;
        }
        .data-table tr:last-child td {
            @apply border-b-0;
        }
        .notes-text {
            @apply bg-amber-50 p-3 rounded-md border border-amber-200 text-sm text-amber-800 mb-4 whitespace-pre-wrap;
        }
        .option-label {
            @apply block p-3 mb-2 border border-gray-300 rounded-md hover:bg-sky-50 cursor-pointer transition-colors;
        }
        .option-label input {
            @apply mr-2;
        }
        .selected-option {
            @apply bg-sky-100 border-sky-400;
        }
        .correct-answer {
            @apply bg-green-100 border-green-400;
        }
        .incorrect-answer {
            @apply bg-red-100 border-red-400;
        }
        .feedback {
            @apply p-4 mt-4 rounded-md text-sm;
        }
        .feedback.correct {
            @apply bg-green-50 text-green-700 border border-green-200;
        }
        .feedback.incorrect {
            @apply bg-red-50 text-red-700 border border-red-200;
        }
        .rationale {
            @apply mt-2 p-3 bg-gray-50 rounded-md border border-gray-200;
        }
        .btn {
            @apply px-6 py-2 rounded-md font-semibold transition-colors text-white;
        }
        .btn-primary {
            @apply bg-sky-600 hover:bg-sky-700;
        }
        .btn-secondary {
            @apply bg-gray-500 hover:bg-gray-600;
        }
        .btn-disabled {
            @apply bg-gray-300 cursor-not-allowed;
        }
        .highlightable {
            @apply p-2 border border-dashed border-gray-300 rounded-md mb-2 cursor-pointer hover:bg-sky-50;
        }
        .highlighted {
            @apply bg-yellow-200 border-yellow-400;
        }
        .clickable-cell {
            @apply p-2 text-center cursor-pointer border border-gray-300 hover:bg-sky-100;
        }
        .selected-cell {
            @apply bg-sky-200 text-sky-800 font-semibold; /* Added text color for better visibility */
        }
        /* Ensure tables within questions are styled */
        #question-details table {
            @apply w-full text-sm text-left text-gray-500 my-4;
        }
        #question-details th {
            @apply px-4 py-2 bg-slate-100 text-slate-700 font-semibold;
        }
        #question-details td {
            @apply px-4 py-2 border-b border-gray-200;
        }
         /* Specific styles for Q2 table */
        #q2-table th, #q2-table td {
            @apply border p-2 text-center;
        }
        #q2-table .clickable-cell:hover {
            @apply bg-sky-100;
        }
        #q2-table .selected-cell {
            @apply bg-sky-300 text-sky-800 font-semibold;
        }
        /* Specific styles for Q4 table */
        #q4-table th, #q4-table td {
            @apply border p-2 text-center;
        }
        #q4-table .clickable-cell:hover {
            @apply bg-sky-100;
        }
        #q4-table .selected-cell {
            @apply bg-sky-300 text-sky-800 font-semibold;
        }
    </style>
</head>
<body class="bg-slate-100 min-h-screen p-4 md:p-8">
    <div class="container mx-auto max-w-4xl">
        <header class="mb-8 text-center">
            <h1 class="text-3xl font-bold text-sky-700">Liver Failure Case Study Quiz</h1>
        </header>

        <div id="case-summary-section" class="content-box">
            <h2 class="section-title">Case Summary</h2>
            <p class="text-sm text-gray-700">
                A 67-year-old male client with a history of alcohol use disorder and a recent episode of binge drinking is admitted to the medical-surgical unit with ascites and symptoms of confusion. The learner should recognize symptoms of worsening cirrhosis and be alert to the development of hepatic encephalopathy and other complications with liver failure, and recognize indicators of changes in condition.
            </p>
        </div>

        <div id="quiz-area" class="content-box">
            </div>

        <div id="navigation-area" class="mt-6 flex justify-between items-center">
            <button id="prev-btn" class="btn btn-secondary" onclick="prevQuestion()" disabled>Previous</button>
            <div id="score-display" class="text-lg font-semibold text-slate-700">Score: 0 / 0</div>
            <button id="next-btn" class="btn btn-primary" onclick="nextQuestion()">Next</button>
            <button id="submit-btn" class="btn btn-primary" onclick="submitAnswer()">Submit Answer</button>
        </div>
    </div>

    <script>
        // --- Quiz Data ---
        const quizData = [
            // Question 1
            {
                id: 1,
                type: 'checkbox', // select multiple
                questionText: "The nurse assesses the client upon admission to the unit. Which 2 findings are the most concerning?",
                notes: "DAY 1 1000. Admitted with ascites and confusion; oriented to person only. Has 25-yr history of alcohol use disorder, mild hypertension, and gastroesophageal reflux disease. Drowsy and dozing off and on, mildly dyspneic, appears thin and malnourished; somewhat agitated answering questions. States has not had a drink in a few weeks; sister who accompanied him notes recent drinking binge a week ago. Placed on oxygen 2 L per nasal cannula. Bulging flanks and peripheral edema noted. Bloodwork sent to lab. Admission weight 142 lbs (64.5 kg).",
                vitals: { headers: ["Time", "Day1: 1000"], rows: [["Temp", "98.4F/36.8C"],["P", "85"],["RR", "22"],["B/P", "142/72"],["Pulse oximeter", "92 on 2L NC"],["Glasgow Coma (3-15)", "12"],["Abdominal girth", "95 cm/37.5in"]] },
                meds: { headers: ["Medication", "Dosage/Frequency/ Route", "Time"], rows: [["metoprolol XL", "50 mg daily", "1000"]] },
                labs: { headers: ["Lab", "Results", "Reference range"], rows: [["BUN", "22 mg/dL", "10-20 mg/dL"],["Glucose (fasting)", "70 mg/dL", "Normal < 99 mg/dL"],["Ammonia", "94 mcg/dL", "10-80 mcg/dL"],["Albumin", "3.2 g/dL", "3.4-5.4 g/dL"]] },
                options: [{ text: "Blood pressure", id: "q1_opt1" },{ text: "BUN", id: "q1_opt2" },{ text: "Neurologic assessment", id: "q1_opt3" },{ text: "Peripheral edema", id: "q1_opt4" },{ text: "Dyspnea", id: "q1_opt5" },{ text: "Albumin level", id: "q1_opt6" },{ text: "Glucose", id: "q1_opt7" }],
                correctAnswers: ["q1_opt3", "q1_opt5"],
                rationale: "The most concerning signs are dyspnea which indicates hepatopulmonary syndrome from worsening ascites, as well as a decline in neurologic function (drowsy off and on, oriented to name only, slightly agitated, etc.). BUN slightly elevated but due to dehydration vs. acute kidney failure as creatinine is normal. A low serum albumin level is expected due to cirrhosis and malnourished condition from alcohol use disorder."
            },
            // Question 2
            {
                id: 2,
                type: 'matrix_click',
                questionText: "For each finding, click to specify if the finding is most consistent with the condition of ascites or elevated ammonia.",
                notes: "DAY 1 1000. Admitted with ascites and confusion; oriented to person only. Has 25-yr history of alcohol use disorder, mild hypertension, and gastroesophageal reflux disease. Drowsy and dozing off and on, mildly dyspneic, appears thin and malnourished; somewhat agitated answering questions. States has not had a drink in a few weeks; sister who accompanied him notes recent drinking binge a week ago. Placed on oxygen 2 L per nasal cannula. Bulging flanks and peripheral edema noted. Bloodwork sent to lab. Admission weight 142 lbs (64.5 kg).",
                vitals: { headers: ["Time", "Day1: 1000"], rows: [["Temp", "98.4F/36.8C"], ["P", "85"], ["RR", "22"], ["B/P", "142/72"], ["Pulse oximeter", "92 on 2L NC"], ["Glasgow Coma (3-15)", "12"], ["Abdominal girth", "95 cm/37.5in"]] },
                meds: { headers: ["Medication", "Dosage/Frequency/ Route", "Time"], rows: [["metoprolol XL", "50 mg daily", "1000"]] },
                labs: { headers: ["Lab", "Results", "Reference range"], rows: [["BUN", "22 mg/dL", "10-20 mg/dL"], ["Glucose (fasting)", "70 mg/dL", "Normal < 99 mg/dL"], ["Ammonia", "94 mcg/dL", "10-80 mcg/dL"], ["Albumin", "3.2 g/dL", "3.4-5.4 g/dL"]] },
                matrix: {
                    rows: [{ finding: "Abdominal girth", id: "q2_r1" },{ finding: "Agitation", id: "q2_r2" },{ finding: "Bulging flanks", id: "q2_r3" },{ finding: "Dozing off and on", id: "q2_r4" },{ finding: "Dyspnea", id: "q2_r5" },{ finding: "Peripheral edema", id: "q2_r6" },{ finding: "Pulse oximetry", id: "q2_r7" },{ finding: "Serum albumin", id: "q2_r8" }],
                    columns: [{ header: "Ascites", id: "ascites" },{ header: "Elevated ammonia", id: "elevated_ammonia" }],
                    correctMapping: { "q2_r1": "ascites", "q2_r2": "elevated_ammonia", "q2_r3": "ascites", "q2_r4": "elevated_ammonia", "q2_r5": "ascites", "q2_r6": "ascites", "q2_r7": "ascites", "q2_r8": "ascites"}
                },
                rationale: "Ascites (a complication of portal hypertension and low albumin from cirrhosis/liver damage) can result in respiratory compromise while deterioration in neurologic status (confusion and agitation) results from increased ammonia levels causing hepatic encephalopathy."
            },
            // Question 3
            {
                id: 3,
                type: 'dropdown_fill',
                questionText: "Complete the following sentence by choosing from the list of options.",
                notes: "DAY 1 1000. Admitted with ascites and confusion; oriented to person only. (Same notes as Q1)",
                vitals: { headers: ["Time", "Day1: 1000"], rows: [["Temp", "98.4F/36.8C"], ["P", "85"], ["RR", "22"], ["B/P", "142/72"], ["Pulse oximeter", "92 on 2L NC"], ["Glasgow Coma (3-15)", "12"], ["Abdominal girth", "95 cm/37.5in"]] },
                meds: { headers: ["Medication", "Dosage/Frequency/ Route", "Time"], rows: [["metoprolol XL", "50 mg daily", "1000"]] },
                labs: { headers: ["Lab", "Results", "Reference range"], rows: [["BUN", "22 mg/dL", "10-20 mg/dL"], ["Glucose (fasting)", "70 mg/dL", "Normal < 99 mg/dL"], ["Ammonia", "94 mcg/dL", "10-80 mcg/dL"], ["Albumin", "3.2 g/dL", "3.4-5.4 g/dL"]] },
                sentenceParts: [
                    { type: "text", content: "The client is most likely experiencing " }, { type: "dropdown", id: "q3_drop1", options: ["esophageal varices", "hepatorenal failure", "hepatic encephalopathy", "acute cholecystitis"], correctAnswer: "hepatic encephalopathy" },
                    { type: "text", content: " as evidenced by " }, { type: "dropdown", id: "q3_drop2", options: ["vital signs", "neurologic assessment", "respiratory assessment", "glucose level"], correctAnswer: "neurologic assessment" },
                    { type: "text", content: "."}
                ],
                rationale: "Hepatic encephalopathy is a common complication of cirrhosis and is caused by inability of the liver to detoxify protein by-products. This results in increased ammonia levels which can be toxic to the CNS. Abnormal neurological findings which are common indicators of hepatic encephalopathy include confusion, lethargy, dozing on and off, restlessness and agitation."
            },
            // Question 4
            {
                id: 4,
                type: 'matrix_indicate',
                questionText: "The client receives the diagnosis of hepatic encephalopathy. For each potential intervention, click to specify whether the intervention is indicated, not indicated, or contraindicated in the plan of care.",
                notes: "DAY 1 1000. (Same notes as Q1)\n1400. Remains alert at times but confused, mumbling off and on; mild hand flap noted. Moderately dyspneic on 2 L nasal oxygen, RR 26. Bulging flanks and prominent veins around umbilicus noted; provider notified.",
                vitals: { headers: ["Time", "Day1: 1000", "Day1: 1400"], rows: [["Temp", "98.4F/36.9C", "98.6F/37C"], ["P", "85", "86"], ["RR", "22", "26"], ["B/P", "142/72", "145/78"], ["Pulse oximeter", "92% on 2L NC", "89% on 2L NC"], ["Glasgow Coma (3-15)", "12", "12"]] },
                labs: { headers: ["Lab", "Results", "Reference range"], rows: [["BUN", "22 mg/dL", "10-20 mg/dL"], ["Glucose (fasting)", "70 mg/dL", "Normal < 99 mg/dL"], ["Ammonia", "94 mcg/dL", "10-80 mcg/dL"], ["Albumin", "3.2 g/dL", "3.4-5.4 g/dL"]] },
                matrix: {
                    rows: [
                        { intervention: "Neuro assessment every 4 hrs", id: "q4_r1" }, { intervention: "Record abdominal girth daily", id: "q4_r2" },
                        { intervention: "Administer acetaminophen 650 mg PRN for temp > 101", id: "q4_r3" }, { intervention: "Monitor pulse oximetry every 4 hrs", id: "q4_r4" },
                        { intervention: "Administer sedative PRN agitation", id: "q4_r5" }, { intervention: "Daily weights", id: "q4_r6" },
                        { intervention: "Supine position when in bed", id: "q4_r7" }, { intervention: "Low sodium diet", id: "q4_r8" },
                        { intervention: "Point of care glucose every 6 hrs", id: "q4_r9" }, { intervention: "Lactulose 30 ml every 4 hrs X 3 doses", id: "q4_r10" }
                    ],
                    columns: [ { header: "Indicated", id: "indicated" }, { header: "Not Indicated", id: "not_indicated" }, { header: "Contraindicated", id: "contraindicated" } ],
                    correctMapping: { "q4_r1": "indicated", "q4_r2": "indicated", "q4_r3": "contraindicated", "q4_r4": "indicated", "q4_r5": "contraindicated", "q4_r6": "indicated", "q4_r7": "contraindicated", "q4_r8": "indicated", "q4_r9": "not_indicated", "q4_r10": "indicated" }
                },
                rationale: "Interventions are focused on treating both ascites and hepatic encephalopathy. Acetaminophen and sedatives are contraindicated as is placing the client flat in bed when dyspneic due to ascites. Glucose monitoring would not harm the client but is not necessary."
            },
            // Question 5
            {
                id: 5,
                type: 'highlight', 
                questionText: "At 1430, the provider assesses the client, reviews the chart and writes orders. Click to highlight the three orders that the nurse should implement immediately.",
                notes: "DAY 1 1000. (Same as Q1)\n1400. (Same as Q4)",
                vitals: { headers: ["Time", "Day1: 1000", "Day1: 1400"], rows: [["Temp", "98.4F/36.9C", "98.6F/37C"],["P", "85", "86"],["RR", "22", "26"],["B/P", "142/72", "145/78"],["Pulse oximeter", "92% on 2L NC", "89% on 2L NC"],["Glasgow Coma (3-15)", "12", "12"]] },
                labs: { headers: ["Lab", "Results", "Reference range"], rows: [["BUN", "22 mg/dL", "10-20 mg/dL"], ["Glucose (fasting)", "70 mg/dL", "Normal < 99 mg/dL"], ["Ammonia", "94 mcg/dL", "10-80 mcg/dL"], ["Albumin", "3.2 g/dL", "3.4-5.4 g/dL"]] },
                orders: [
                    { text: "VS, pulse oximetry and neuro assessment every 4 hours and PRN", id: "q5_ord1"}, { text: "Low sodium diet", id: "q5_ord2"},
                    { text: "Record weight & abdominal girth daily", id: "q5_ord3"}, { text: "Oxygen per nasal cannula to maintain pulse oximetry at 95 or greater", id: "q5_ord4"},
                    { text: "IV normal saline at 30 ml/hr", id: "q5_ord5"}, { text: "Lactulose 30 ml PO every 4 hrs X 3 doses", id: "q5_ord6"},
                    { text: "Furosemide 20 mg IV", id: "q5_ord7"}, { text: "Spironolactone 100 mg PO daily", id: "q5_ord8"}
                ],
                correctAnswers: ["q5_ord4", "q5_ord6", "q5_ord7"], 
                maxSelections: 3,
                rationale: "Priorities are to reduce the ammonia level with first dose of lactulose and promote prompt diuresis of excess fluid with IV furosemide. Oxygenation is another priority so increasing his oxygen in meantime to improve pulse oximetry/oxygenation."
            },
            // Question 6
            {
                id: 6,
                type: 'dropdown_fill',
                questionText: "On the second day, the nurse documents and reviews the morning vital signs, urine output and updated ammonia level after implementing the treatment plan. Complete the following sentence by choosing from the list of options.",
                notes: "DAY 1 1000. (Same as Q1)\n1400. (Same as Q4)\n1700 Pulse oximetry 93% on 4 L oxygen. 2nd dose lactulose given; 2 large loose brown stools since first dose. Alert, coherent and cooperative with assessment. 400 ml urine output since 1400.\nDAY 2 0900: Pulse oximetry 95 on RA; no dyspnea noted. Alert and oriented X3 with no signs of agitation. Urine clear yellow at 30-40 ml/hr since 0600. Weight 138 lbs (62.7 kg) and abd. girth recorded. Am medications (metoprolol and spironolactone) given. Ammonia level now 72.",
                vitals: { headers: ["Time", "Day1: 1000", "Day1: 1400", "Day1: 1800", "Day 2 0800"], rows: [["Temp", "98.4F/36.9C", "98.6F/37C", "97.8F/36.5C", "98.6F/37C"], ["P", "85", "86", "88", "85"], ["RR", "22", "26", "18", "16"], ["B/P", "142/72", "145/78", "139/72", "132/64"], ["Pulse oximeter", "92% on 2L NC", "89% on 2L NC", "93% on 4L NC", "95% on RA"], ["Glasgow Coma (3-15)", "12", "12", "14", "14"], ["Abdominal girth", "95 cm/37.5in", "", "", "88 cm / 34.5in"]] },
                labs: { headers: ["Lab", "Results", "Reference range", "Updated (Day 2)"], rows: [["BUN", "22 mg/dL", "10-20 mg/dL", ""], ["Glucose (fasting)", "70 mg/dL", "Normal < 99 mg/dL", ""], ["Ammonia", "94 mcg/dL", "10-80 mcg/dL", "72 mcg/dL"], ["Albumin", "3.2 g/dL", "3.4-5.4 g/dL", ""]] },
                sentenceParts: [
                    { type: "text", content: "The nurse determines the client’s status is " }, { type: "dropdown", id: "q6_drop1", options: ["Improving", "Deteriorating", "Unchanged"], correctAnswer: "Improving" },
                    { type: "text", content: ". The nurse should now " }, { type: "dropdown", id: "q6_drop2", options: ["Request order for more lactulose", "Apply restraints", "Explore readiness to stop drinking"], correctAnswer: "Explore readiness to stop drinking" },
                    { type: "text", content: "."}
                ],
                rationale: "Client’s overall condition has improved. Prescribed interventions of IV furosemide and sodium restriction were effective in reducing ascites; the ammonia level and neurologic status also improved after 3 doses of lactulose."
            },
            // Bowtie Question
             {
                id: 7, 
                type: 'bowtie_select',
                questionText: "Complete the diagram by selecting from the choices below to specify what condition the client is most likely experiencing, 2 actions the nurse should take to address that condition, and 2 parameters the nurse should monitor to assess the client’s progress.",
                notes: "DAY 1 1000. Admitted with ascites and confusion; oriented to person only. (Same as Q1)",
                vitals: { headers: ["Time", "Day1: 1000"], rows: [["Temp", "98.4F/36.8C"], ["P", "85"], ["RR", "22"], ["B/P", "142/72"], ["Pulse oximeter", "92 on 2L NC"], ["Glasgow Coma (3-15)", "12"], ["Abdominal girth", "95 cm/37.5in"]] },
                labs: { headers: ["Lab", "Results", "Reference range"], rows: [["BUN", "22 mg/dL", "10-20 mg/dL"], ["Glucose (fasting)", "70 mg/dL", "Normal < 99 mg/dL"], ["Ammonia", "94 mcg/dL", "10-80 mcg/dL"], ["Albumin", "3.2 g/dL", "3.4-5.4 g/dL"]] },
                bowtieSections: {
                    condition: { label: "Condition most likely experiencing:", id: "bowtie_condition", options: ["Esophageal varices", "Hepatic encephalopathy", "Acute cholecystitis", "Acute alcohol intoxication"], correctAnswer: "Hepatic encephalopathy" },
                    actions: { label: "Actions to take (select 2):", id_prefix: "bowtie_action_", options: ["Administer lactulose", "Request order for sedative", "Institute safety precautions", "Administer IV furosemide", "Educate patient about alcohol cessation"], correctAnswers: ["Administer lactulose", "Institute safety precautions"], maxSelections: 2 },
                    parameters: { label: "Parameters to monitor (select 2):", id_prefix: "bowtie_parameter_", options: ["Serum glucose", "Neurologic status", "Serum ammonia", "Serum creatinine", "Blood pressure"], correctAnswers: ["Neurologic status", "Serum ammonia"], maxSelections: 2 }
                },
                rationale: "Based on neurologic status/confusion and agitation due to elevated ammonia level, the client is experiencing hepatic encephalopathy. Interventions include giving lactulose to lower ammonia levels by inducing diarrhea and maintaining safety/preventing injury until confusion and agitation subsides. While furosemide may be ordered the purpose of this medication is to reduce ascites and alleviate potential for pulmonary complications. Sedatives are contraindicated in persons with liver failure. Client is acutely ill therefore not appropriate to perform education on alcohol cessation until more stable and when readiness can be assessed."
            }
        ];

        // --- Quiz State ---
        let currentQuestionIndex = 0;
        let score = 0;
        let userAnswers = {}; 

        // --- DOM Elements ---
        const quizArea = document.getElementById('quiz-area');
        const prevBtn = document.getElementById('prev-btn');
        const nextBtn = document.getElementById('next-btn');
        const submitBtn = document.getElementById('submit-btn');
        const scoreDisplay = document.getElementById('score-display');

        // --- Helper Functions ---
        function renderTable(data, title) {
            if (!data || !data.headers || !data.rows) return '';
            let tableHtml = `<div class="data-table mb-4"><h3 class="text-md font-semibold text-slate-600 mb-1">${title}</h3><table><thead><tr>`;
            data.headers.forEach(header => tableHtml += `<th>${header}</th>`);
            tableHtml += `</tr></thead><tbody>`;
            data.rows.forEach(row => {
                tableHtml += `<tr>`;
                row.forEach(cell => tableHtml += `<td>${cell || ''}</td>`);
                tableHtml += `</tr>`;
            });
            tableHtml += `</tbody></table></div>`;
            return tableHtml;
        }
        
        function renderQuestion() {
            const question = quizData[currentQuestionIndex];
            let html = `<div id="question-content" data-question-id="${question.id}">`;

            if (question.notes) { html += `<div class="content-box bg-gray-50"><h3 class="section-title">Nurses’ Notes</h3><p class="notes-text">${question.notes}</p></div>`; }
            if (question.vitals) { html += `<div class="content-box bg-gray-50">${renderTable(question.vitals, "Vital Signs")}</div>`; }
            if (question.meds) { html += `<div class="content-box bg-gray-50">${renderTable(question.meds, "Medications")}</div>`; }
            if (question.labs) { html += `<div class="content-box bg-gray-50">${renderTable(question.labs, "Laboratory Report")}</div>`; }
            
            html += `<h2 class="question-title mt-4">${currentQuestionIndex + 1}. ${question.questionText}</h2>`;
            html += `<div id="question-options">`;

            if (question.type === 'checkbox' || question.type === 'radio') {
                question.options.forEach(opt => {
                    html += `<label class="option-label" for="${opt.id}"><input type="${question.type}" name="q${question.id}_option" id="${opt.id}" value="${opt.id}"> ${opt.text}</label>`;
                });
            } else if (question.type === 'matrix_click' || question.type === 'matrix_indicate') {
                const tableId = question.type === 'matrix_click' ? 'q2-table' : 'q4-table';
                html += `<table id="${tableId}" class="w-full border-collapse border border-gray-300 my-4"><thead><tr><th>${question.type === 'matrix_click' ? 'Assessment/Finding' : 'Potential Intervention'}</th>`;
                question.matrix.columns.forEach(col => html += `<th>${col.header}</th>`);
                html += `</tr></thead><tbody>`;
                question.matrix.rows.forEach(row => {
                    html += `<tr><td class="font-medium p-2 border ${question.type === 'matrix_indicate' ? 'text-left' : ''}">${row.finding || row.intervention}</td>`;
                    question.matrix.columns.forEach(col => {
                        html += `<td class="clickable-cell" data-row-id="${row.id}" data-col-id="${col.id}" onclick="handleMatrixClick(this, '${row.id}')"></td>`;
                    });
                    html += `</tr>`;
                });
                html += `</tbody></table>`;
                if (!userAnswers[question.id]) userAnswers[question.id] = {}; // Ensure initialized
            } else if (question.type === 'dropdown_fill') {
                html += `<p class="text-lg text-slate-700 leading-relaxed">`;
                question.sentenceParts.forEach(part => {
                    if (part.type === 'text') { html += part.content; } 
                    else if (part.type === 'dropdown') {
                        html += `<select id="${part.id}" class="p-2 border border-gray-300 rounded-md mx-1"><option value="">Select...</option>`;
                        part.options.forEach(opt => html += `<option value="${opt}">${opt}</option>`);
                        html += `</select>`;
                    }
                });
                html += `</p>`;
            } else if (question.type === 'highlight') {
                question.orders.forEach(order => {
                    html += `<div class="highlightable" data-order-id="${order.id}" onclick="toggleHighlight(this, ${question.maxSelections})">${order.text}</div>`;
                });
                if (!userAnswers[question.id]) userAnswers[question.id] = []; // Ensure initialized
            } else if (question.type === 'bowtie_select') {
                const { condition, actions, parameters } = question.bowtieSections;
                html += `<div class="mb-4"><label class="block font-semibold mb-1" for="${condition.id}">${condition.label}</label><select id="${condition.id}" class="w-full p-2 border border-gray-300 rounded-md"><option value="">Select Condition...</option>`;
                condition.options.forEach(opt => html += `<option value="${opt}">${opt}</option>`);
                html += `</select></div>`;
                html += `<div class="mb-4"><p class="font-semibold mb-1">${actions.label}</p>`;
                actions.options.forEach((opt, i) => html += `<label class="option-label" for="${actions.id_prefix}${i}"><input type="checkbox" name="bowtie_actions" id="${actions.id_prefix}${i}" value="${opt}" data-max-selections="${actions.maxSelections}"> ${opt}</label>`);
                html += `</div>`;
                html += `<div class="mb-4"><p class="font-semibold mb-1">${parameters.label}</p>`;
                parameters.options.forEach((opt, i) => html += `<label class="option-label" for="${parameters.id_prefix}${i}"><input type="checkbox" name="bowtie_parameters" id="${parameters.id_prefix}${i}" value="${opt}" data-max-selections="${parameters.maxSelections}"> ${opt}</label>`);
                html += `</div>`;
            }

            html += `</div><div id="feedback-area" class="mt-4"></div></div>`;
            quizArea.innerHTML = html;

            document.querySelectorAll('#question-options input[type="checkbox"], #question-options input[type="radio"]').forEach(input => {
                input.addEventListener('change', (event) => {
                    const label = event.target.closest('.option-label');
                    if (question.type === 'radio') {
                        document.querySelectorAll(`input[name="${event.target.name}"]`).forEach(radio => radio.closest('.option-label').classList.remove('selected-option'));
                    }
                    label.classList.toggle('selected-option', event.target.checked);
                });
            });
            
            if (question.type === 'bowtie_select') {
                ['bowtie_actions', 'bowtie_parameters'].forEach(groupName => {
                    document.querySelectorAll(`input[name="${groupName}"]`).forEach(checkbox => {
                        checkbox.addEventListener('change', (event) => {
                            const max = parseInt(event.target.dataset.maxSelections);
                            const checkedCount = Array.from(document.querySelectorAll(`input[name="${groupName}"]:checked`)).length;
                            if (checkedCount > max) {
                                event.target.checked = false;
                                alert(`You can only select up to ${max} options for this section.`);
                            }
                            event.target.closest('.option-label').classList.toggle('selected-option', event.target.checked);
                        });
                    });
                });
            }
            updateNavigation();
        }

        function handleMatrixClick(cellElement, rowId) {
            console.log('handleMatrixClick called for rowId:', rowId, 'cell:', cellElement); // DIAGNOSTIC
            const question = quizData[currentQuestionIndex];
            if (!question) {
                console.error('handleMatrixClick: current question is undefined'); // DIAGNOSTIC
                return;
            }
            console.log('Current question ID for matrix:', question.id); // DIAGNOSTIC

            const qId = question.id;
            const colId = cellElement.dataset.colId;
            console.log('Selected columnId:', colId); // DIAGNOSTIC

            // Ensure userAnswers[qId] is an object
            if (typeof userAnswers[qId] !== 'object' || userAnswers[qId] === null) {
                console.log('Initializing userAnswers for qId as object:', qId); // DIAGNOSTIC
                userAnswers[qId] = {};
            }

            const rowElement = cellElement.parentElement;
            if (rowElement) {
                // console.log('Row element for matrix click:', rowElement); // DIAGNOSTIC (can be verbose)
                rowElement.querySelectorAll('td.clickable-cell').forEach(cell => {
                    cell.classList.remove('selected-cell');
                });
            } else {
                console.error('Could not find parentElement for cell:', cellElement); // DIAGNOSTIC
            }
            
            cellElement.classList.add('selected-cell');
            console.log('Added selected-cell to:', cellElement); // DIAGNOSTIC
            userAnswers[qId][rowId] = colId;
            console.log('Updated userAnswers (matrix):', JSON.parse(JSON.stringify(userAnswers))); // DIAGNOSTIC
        }

        function toggleHighlight(element, maxSelections) {
            console.log('toggleHighlight called for element:', element, 'maxSelections:', maxSelections); // DIAGNOSTIC
            const question = quizData[currentQuestionIndex];
            if (!question) {
                console.error('toggleHighlight: current question is undefined'); // DIAGNOSTIC
                return;
            }
            console.log('Current question ID for highlight:', question.id); // DIAGNOSTIC

            const qId = question.id;
            const orderId = element.dataset.orderId;
            console.log('Selected orderId:', orderId); // DIAGNOSTIC

            // Ensure userAnswers[qId] is an array
            if (!Array.isArray(userAnswers[qId])) {
                console.log('Initializing userAnswers for qId as array:', qId); // DIAGNOSTIC
                userAnswers[qId] = [];
            }
            
            let selections = userAnswers[qId];
            const index = selections.indexOf(orderId);

            if (index > -1) { // Already selected, unselect
                console.log('Unselecting orderId:', orderId); // DIAGNOSTIC
                element.classList.remove('highlighted');
                selections.splice(index, 1);
            } else { // Not selected, select if under max
                if (selections.length < maxSelections) {
                    console.log('Selecting orderId:', orderId); // DIAGNOSTIC
                    element.classList.add('highlighted');
                    selections.push(orderId);
                } else {
                    console.log('Max selections reached for orderId:', orderId); // DIAGNOSTIC
                    alert(`You can only select up to ${maxSelections} orders.`);
                }
            }
            console.log('Updated userAnswers (highlight):', JSON.parse(JSON.stringify(userAnswers))); // DIAGNOSTIC
        }

        function updateNavigation() {
            prevBtn.disabled = currentQuestionIndex === 0;
            const questionSubmitted = userAnswers.hasOwnProperty(quizData[currentQuestionIndex].id + '_submitted');
            nextBtn.disabled = questionSubmitted ? (currentQuestionIndex === quizData.length - 1 && !userAnswers.hasOwnProperty('final_score_shown')) : true;

            submitBtn.style.display = questionSubmitted ? 'none' : 'inline-block';
            
            if (currentQuestionIndex === quizData.length - 1 && questionSubmitted) {
                 nextBtn.textContent = 'Show Final Score';
                 nextBtn.disabled = false; 
            } else {
                nextBtn.textContent = 'Next';
            }
            scoreDisplay.textContent = `Score: ${score} / ${quizData.filter(q => userAnswers[q.id + '_submitted']).length}`;
        }

        function submitAnswer() {
            const question = quizData[currentQuestionIndex];
            const feedbackArea = document.getElementById('feedback-area');
            let isCorrect = false;
            let selectedAnswers = []; 

            if (question.type === 'checkbox') {
                selectedAnswers = Array.from(document.querySelectorAll(`#question-options input[type="checkbox"]:checked`)).map(cb => cb.value);
                isCorrect = question.correctAnswers.length === selectedAnswers.length && question.correctAnswers.every(ans => selectedAnswers.includes(ans));
            } else if (question.type === 'radio') {
                const selRadio = document.querySelector(`#question-options input[type="radio"]:checked`);
                if (selRadio) { selectedAnswers = [selRadio.value]; isCorrect = question.correctAnswers.includes(selRadio.value); }
            } else if (question.type === 'matrix_click' || question.type === 'matrix_indicate') {
                const userSelections = userAnswers[question.id];
                isCorrect = true; 
                if (!userSelections || typeof userSelections !== 'object') {
                    isCorrect = false;
                    console.warn("SubmitAnswer Matrix: userSelections is not an object or undefined for Q_ID:", question.id, userSelections); // DIAGNOSTIC
                } else {
                    const correctKeys = Object.keys(question.matrix.correctMapping);
                    const userKeys = Object.keys(userSelections);
                    if (userKeys.length !== correctKeys.length) { 
                        isCorrect = false;
                        console.warn("SubmitAnswer Matrix: Mismatch in number of answered rows for Q_ID:", question.id, "User:", userKeys.length, "Expected:", correctKeys.length); // DIAGNOSTIC
                    } else {
                        for (const rowId of correctKeys) {
                            if (!userSelections.hasOwnProperty(rowId) || userSelections[rowId] !== question.matrix.correctMapping[rowId]) {
                                isCorrect = false;
                                console.warn("SubmitAnswer Matrix: Incorrect answer or missing row for Q_ID:", question.id, "RowID:", rowId, "User:", userSelections[rowId], "Correct:", question.matrix.correctMapping[rowId]); // DIAGNOSTIC
                                break;
                            }
                        }
                    }
                }
            } else if (question.type === 'dropdown_fill') {
                isCorrect = true;
                question.sentenceParts.forEach(part => {
                    if (part.type === 'dropdown') {
                        const val = document.getElementById(part.id).value;
                        if (val !== part.correctAnswer) isCorrect = false;
                    }
                });
            } else if (question.type === 'highlight') {
                selectedAnswers = userAnswers[question.id] || [];
                isCorrect = question.correctAnswers.length === selectedAnswers.length && question.correctAnswers.every(ans => selectedAnswers.includes(ans));
            } else if (question.type === 'bowtie_select') {
                isCorrect = true;
                const { condition, actions, parameters } = question.bowtieSections;
                if (document.getElementById(condition.id).value !== condition.correctAnswer) isCorrect = false;
                
                const selActions = Array.from(document.querySelectorAll('input[name="bowtie_actions"]:checked')).map(cb => cb.value);
                if (!(selActions.length === actions.correctAnswers.length && actions.correctAnswers.every(ans => selActions.includes(ans)))) isCorrect = false;
                
                const selParams = Array.from(document.querySelectorAll('input[name="bowtie_parameters"]:checked')).map(cb => cb.value);
                if (!(selParams.length === parameters.correctAnswers.length && parameters.correctAnswers.every(ans => selParams.includes(ans)))) isCorrect = false;
            }

            userAnswers[question.id + '_submitted'] = true; 
            if (isCorrect) {
                score++;
                feedbackArea.innerHTML = `<div class="feedback correct"><strong>Correct!</strong><div class="rationale"><strong>Rationale:</strong> ${question.rationale}</div></div>`;
            } else {
                feedbackArea.innerHTML = `<div class="feedback incorrect"><strong>Incorrect.</strong><div class="rationale"><strong>Rationale:</strong> ${question.rationale}</div></div>`;
            }
            
            if (question.type === 'checkbox' || question.type === 'radio') {
                question.options.forEach(opt => {
                    const label = document.querySelector(`label[for="${opt.id}"]`);
                    const input = document.getElementById(opt.id);
                    label.classList.remove('selected-option');
                    if (question.correctAnswers.includes(opt.id)) label.classList.add('correct-answer');
                    if (input.checked && !question.correctAnswers.includes(opt.id)) label.classList.add('incorrect-answer');
                });
            } else if (question.type === 'highlight') {
                question.orders.forEach(order => {
                    const div = document.querySelector(`.highlightable[data-order-id="${order.id}"]`);
                    if (div) { // Ensure div exists
                        if (question.correctAnswers.includes(order.id)) div.classList.add('correct-answer');
                        if (div.classList.contains('highlighted') && !question.correctAnswers.includes(order.id)) div.classList.add('incorrect-answer');
                        div.classList.remove('highlighted'); 
                    }
                });
            } else if (question.type === 'matrix_click' || question.type === 'matrix_indicate') {
                // Add visual feedback for matrix answers after submission
                const userSelections = userAnswers[question.id];
                question.matrix.rows.forEach(row => {
                    const rowElement = document.querySelector(`#${question.type === 'matrix_click' ? 'q2-table' : 'q4-table'} td[data-row-id="${row.id}"]`)?.parentElement;
                    if (rowElement) {
                        rowElement.querySelectorAll('td.clickable-cell').forEach(cell => {
                            const colId = cell.dataset.colId;
                            if (userSelections && userSelections[row.id] === colId) { // Cell was selected by user
                                if (question.matrix.correctMapping[row.id] === colId) {
                                    cell.classList.add('correct-answer');
                                } else {
                                    cell.classList.add('incorrect-answer');
                                }
                            } else if (question.matrix.correctMapping[row.id] === colId) { // Cell is correct but wasn't selected by user
                                // Optionally highlight the correct cell if user missed it or chose wrong
                                // cell.classList.add('correct-missed'); // Needs a style
                            }
                            cell.classList.remove('selected-cell'); // Remove temporary selection style
                        });
                    }
                });
            }
            
            document.querySelectorAll('#question-options input, #question-options select, .highlightable, .clickable-cell').forEach(el => {
                el.disabled = true;
                if (el.classList.contains('highlightable') || el.classList.contains('clickable-cell')) el.style.pointerEvents = 'none';
            });

            updateNavigation();
        }

        function nextQuestion() {
            if (currentQuestionIndex < quizData.length - 1) {
                currentQuestionIndex++;
                renderQuestion();
            } else {
                userAnswers['final_score_shown'] = true; 
                quizArea.innerHTML = `<div class="text-center">
                                        <h2 class="text-2xl font-bold text-sky-700 mb-4">Quiz Completed!</h2>
                                        <p class="text-xl text-slate-700">Your final score is: ${score} out of ${quizData.length}</p>
                                        <button class="btn btn-primary mt-6" onclick="restartQuiz()">Restart Quiz</button>
                                      </div>`;
                prevBtn.style.display = 'none';
                nextBtn.style.display = 'none';
                submitBtn.style.display = 'none';
                scoreDisplay.textContent = `Final Score: ${score} / ${quizData.length}`;
            }
        }

        function prevQuestion() {
            if (currentQuestionIndex > 0) {
                if (userAnswers.hasOwnProperty('final_score_shown')) delete userAnswers['final_score_shown'];
                currentQuestionIndex--;
                renderQuestion();
                 if (userAnswers.hasOwnProperty(quizData[currentQuestionIndex].id + '_submitted')) {
                    submitBtn.style.display = 'none';
                    nextBtn.disabled = false;
                    const question = quizData[currentQuestionIndex];
                    const feedbackArea = document.getElementById('feedback-area');
                    if (feedbackArea) {
                        // Re-apply the feedback and visual indicators for correct/incorrect
                        // This requires re-running parts of submitAnswer's feedback logic
                        // For simplicity, we'll just show the rationale and disable elements.
                        // A more robust solution would store the feedback HTML or re-evaluate.
                        let tempIsCorrect = false; // Re-evaluate to show correct/incorrect styling
                        // Note: This re-evaluation is partial and might not cover all visual states perfectly without full state restoration.
                        if (question.type === 'matrix_click' || question.type === 'matrix_indicate') {
                            const userSelections = userAnswers[question.id];
                            tempIsCorrect = true;
                            if (!userSelections || typeof userSelections !== 'object') tempIsCorrect = false;
                            else {
                                const correctKeys = Object.keys(question.matrix.correctMapping);
                                if (Object.keys(userSelections).length !== correctKeys.length) tempIsCorrect = false;
                                else {
                                    for (const rowId of correctKeys) {
                                        if (!userSelections.hasOwnProperty(rowId) || userSelections[rowId] !== question.matrix.correctMapping[rowId]) {
                                            tempIsCorrect = false; break;
                                        }
                                    }
                                }
                            }
                        } else if (question.type === 'highlight') {
                             const selectedAnswers = userAnswers[question.id] || [];
                             tempIsCorrect = question.correctAnswers.length === selectedAnswers.length && question.correctAnswers.every(ans => selectedAnswers.includes(ans));
                        } // Add other types if needed for full visual restoration

                        if (userAnswers[question.id + '_submitted_correctly']) { // Assuming we stored this
                             feedbackArea.innerHTML = `<div class="feedback correct"><strong>Correct!</strong><div class="rationale"><strong>Rationale:</strong> ${question.rationale}</div></div>`;
                        } else {
                             feedbackArea.innerHTML = `<div class="feedback incorrect"><strong>Incorrect.</strong><div class="rationale"><strong>Rationale:</strong> ${question.rationale}</div></div>`;
                        }
                        // Re-apply visual styles to options (correct/incorrect)
                        // This part is complex to do perfectly without storing the full DOM state or re-running full submit logic.
                        // The current simplified approach in submitAnswer for matrix/highlight feedback after submission might be sufficient.
                    }
                     document.querySelectorAll('#question-options input, #question-options select, .highlightable, .clickable-cell').forEach(el => {
                        el.disabled = true;
                        if (el.classList.contains('highlightable') || el.classList.contains('clickable-cell')) el.style.pointerEvents = 'none';
                    });
                }
            }
        }
        
        function restartQuiz() {
            currentQuestionIndex = 0;
            score = 0;
            userAnswers = {};
            prevBtn.style.display = 'inline-block'; 
            nextBtn.style.display = 'inline-block'; 
            renderQuestion();
        }

        // --- Initial Load ---
        renderQuestion();
    </script>
</body>
</html>
