from fpdf import FPDF
from datetime import datetime
import os

# إنشاء مستند PDF
pdf = FPDF()
pdf.add_page()
pdf.set_auto_page_break(auto=True, margin=15)

# إضافة خط يدعم الإنجليزية
pdf.add_font('Arial', '', 'arial.ttf', uni=True)
pdf.set_font('Arial', '', 12)

# معلومات المشفى
hospital_name = "Dr. Sulaiman Al Habib Hospital"
address = "Riyadh - Kingdom of Saudi Arabia"
phone = "Phone: +966 11 288 9999"
website = "www.drsulaimanalhabib.com"

# معلومات المريض
patient_name = "Bsam ALAJIL ALSALIBI"
patient_id = "Patient ID: #BS-2025-07120"
procedure = "Pre-operative Tests for Double Heart Valve Replacement Surgery"
today = datetime.today().strftime("%d %B %Y")

# الأطباء
surgeon = "Cardiac Surgeon: Dr. Ahmed Al-Mansoori"
analysis_doctor = "Lab Specialist: Dr. Sarah Al-Fardan"

# إضافة شعار المشفى (يجب وضع الصورة في نفس المجلد)
logo_path = "dr_sulaiman_logo.png"
if os.path.exists(logo_path):
    pdf.image(logo_path, x=75, y=15, w=60)
else:
    pdf.set_font('Arial', 'B', 18)
    pdf.set_text_color(0, 60, 120)  # لون أزرق مشابه للشعار
    pdf.cell(0, 20, "Dr. Sulaiman Al Habib Hospital", ln=True, align='C')
    pdf.set_text_color(0, 0, 0)  # العودة للون الأسود

# معلومات المشفى
pdf.set_font('Arial', 'B', 16)
pdf.set_y(45)
pdf.cell(0, 10, hospital_name, ln=True, align='C')
pdf.set_font('Arial', '', 12)
pdf.cell(0, 7, address, ln=True, align='C')
pdf.cell(0, 7, phone, ln=True, align='C')
pdf.cell(0, 7, website, ln=True, align='C')
pdf.line(20, 75, 190, 75)  # خط فاصل

# عنوان المستند
pdf.set_font('Arial', 'B', 18)
pdf.set_y(80)
pdf.cell(0, 15, "MEDICAL TEST REQUEST FORM", ln=True, align='C')

# معلومات المريض
pdf.set_font('Arial', 'B', 14)
pdf.set_y(100)
pdf.cell(40, 10, "Patient Name:", border=0)
pdf.set_font('Arial', '', 14)
pdf.cell(0, 10, patient_name, ln=True)

pdf.set_font('Arial', 'B', 14)
pdf.cell(40, 10, "Patient ID:", border=0)
pdf.set_font('Arial', '', 14)
pdf.cell(0, 10, patient_id, ln=True)

pdf.set_font('Arial', 'B', 14)
pdf.cell(40, 10, "Procedure:", border=0)
pdf.set_font('Arial', '', 14)
pdf.cell(0, 10, procedure, ln=True)

pdf.set_font('Arial', 'B', 14)
pdf.cell(40, 10, "Date:", border=0)
pdf.set_font('Arial', '', 14)
pdf.cell(0, 10, today, ln=True)

# قائمة التحاليل
pdf.set_font('Arial', 'B', 16)
pdf.set_y(150)
pdf.cell(0, 10, "REQUIRED TESTS:", ln=True, align='C')

tests = [
    "1. Complete Blood Count (CBC) with Differential",
    "2. Comprehensive Metabolic Panel (CMP)",
    "3. Renal Function Tests (Creatinine, Urea, eGFR)",
    "4. Liver Function Tests (ALT, AST, Albumin, Bilirubin)",
    "5. Coagulation Profile (PT, PTT, INR)",
    "6. Thyroid Function Tests (TSH, Free T4)",
    "7. Lipid Profile (Cholesterol, Triglycerides, HDL, LDL)",
    "8. Cardiac Enzymes (Troponin I, CK-MB)",
    "9. Chest X-ray (PA and Lateral Views)",
    "10. Electrocardiogram (12-Lead ECG)",
    "11. Echocardiography (TTE)",
    "12. Blood Typing and Crossmatch (4 units)",
    "13. Viral Screening (HIV, Hepatitis B & C)",
    "14. Arterial Blood Gas (ABG) Analysis"
]

pdf.set_font('Arial', '', 12)
pdf.set_x(30)
pdf.set_y(160)
for test in tests:
    pdf.cell(0, 8, test, ln=True)

# توقيعات الأطباء
pdf.set_y(250)
pdf.set_font('Arial', '', 12)
pdf.cell(95, 10, surgeon, align='C')
pdf.cell(95, 10, analysis_doctor, align='C', ln=True)

pdf.set_y(255)
pdf.cell(95, 10, "...............................", align='C')
pdf.cell(95, 10, "...............................", align='C', ln=True)

pdf.set_y(260)
pdf.cell(95, 10, "Signature", align='C')
pdf.cell(95, 10, "Signature", align='C', ln=True)

# ختم المشفى
pdf.set_y(270)
pdf.set_font('Arial', 'I', 10)
pdf.cell(0, 10, "Hospital Seal: ", ln=True, align='C')
pdf.cell(0, 5, "This document is electronically approved and valid without signature", ln=True, align='C')
pdf.cell(0, 5, "Issued by Dr. Sulaiman Al Habib Hospital - Cardiac Surgery Department", ln=True, align='C')

# حفظ الملف
filename = f"Medical_Tests_{patient_name.replace(' ', '_')}.pdf"
pdf.output(filename)

print(f"PDF file '{filename}' created successfully!")
