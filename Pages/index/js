import React, { useState, useMemo } from "react";
import { Card, CardContent } from "@/components/ui/card";
import { Button } from "@/components/ui/button";
import { Input } from "@/components/ui/input";
import { Select, SelectItem } from "@/components/ui/select";

export default function WellthMatchQuiz() {
  const [step, setStep] = useState(1);
  const [formData, setFormData] = useState({
    age: "",
    income: "",
    assets: "",
    goals: "",
    zip: "",
    name: "",
    email: "",
    phone: ""
  });
  const [submitted, setSubmitted] = useState(false);
  const [matchedAdvisor, setMatchedAdvisor] = useState(null);

  const handleChange = (e) => {
    setFormData({ ...formData, [e.target.name]: e.target.value });
  };

  const isStepValid = () => {
    const fieldKeys = ["age", "income", "assets", "goals", "zip", "name", "email", "phone"];
    return formData[fieldKeys[step - 1]] !== "";
  };

  const handleNext = () => {
    if (isStepValid()) setStep(step + 1);
  };

  const handleBack = () => setStep(step - 1);

  const handleSubmit = (e) => {
    e.preventDefault();
    const advisor = matchAdvisor(formData.zip, formData.assets);
    setMatchedAdvisor(advisor);
    setSubmitted(true);
    console.log("WellthMatch Lead:", formData);
  };

  const matchAdvisor = (zip, assets) => {
    const assetLevel = assets.includes("$500,000") || assets.includes("$1,000,000") ? "high" : "standard";
    if (zip.startsWith("9") && assetLevel === "high") {
      return { name: "Alex Morgan", firm: "Pacific Wealth Group", contact: "alex@pacwealth.com" };
    } else if (zip.startsWith("7")) {
      return { name: "Jamie Lee", firm: "Southern Oak Advisors", contact: "jamie@southernoak.com" };
    } else {
      return { name: "Taylor Reed", firm: "Nationwide Financial Partners", contact: "taylor@nfp.com" };
    }
  };

  const steps = useMemo(() => [
    <div key="1">
      <label className="block mb-2">What is your age?</label>
      <Input name="age" type="number" onChange={handleChange} value={formData.age} required />
    </div>,
    <div key="2">
      <label className="block mb-2">What is your annual income?</label>
      <Select name="income" onValueChange={(value) => setFormData({ ...formData, income: value })} value={formData.income} required>
        <SelectItem value="" disabled>Select income range</SelectItem>
        <SelectItem value="Under $50,000">Under $50,000</SelectItem>
        <SelectItem value="$50,000 - $99,999">$50,000 - $99,999</SelectItem>
        <SelectItem value="$100,000 - $249,999">$100,000 - $249,999</SelectItem>
        <SelectItem value="$250,000 - $499,999">$250,000 - $499,999</SelectItem>
        <SelectItem value="$500,000+">$500,000+</SelectItem>
      </Select>
    </div>,
    <div key="3">
      <label className="block mb-2">What is the total value of your investments/savings?</label>
      <Select name="assets" onValueChange={(value) => setFormData({ ...formData, assets: value })} value={formData.assets} required>
        <SelectItem value="" disabled>Select asset range</SelectItem>
        <SelectItem value="Under $50,000">Under $50,000</SelectItem>
        <SelectItem value="$50,000 - $249,999">$50,000 - $249,999</SelectItem>
        <SelectItem value="$250,000 - $499,999">$250,000 - $499,999</SelectItem>
        <SelectItem value="$500,000 - $999,999">$500,000 - $999,999</SelectItem>
        <SelectItem value="$1,000,000+">$1,000,000+</SelectItem>
      </Select>
    </div>,
    <div key="4">
      <label className="block mb-2">What is your primary financial goal?</label>
      <Select name="goals" onValueChange={(value) => setFormData({ ...formData, goals: value })} value={formData.goals} required>
        <SelectItem value="" disabled>Select your goal</SelectItem>
        <SelectItem value="Retirement Planning">Retirement Planning</SelectItem>
        <SelectItem value="Saving for a Home">Saving for a Home</SelectItem>
        <SelectItem value="College Savings">College Savings</SelectItem>
        <SelectItem value="Investment Growth">Investment Growth</SelectItem>
        <SelectItem value="Debt Reduction">Debt Reduction</SelectItem>
      </Select>
    </div>,
    <div key="5">
      <label className="block mb-2">What is your ZIP code?</label>
      <Input name="zip" type="text" onChange={handleChange} value={formData.zip} required />
    </div>,
    <div key="6">
      <label className="block mb-2">Your Name</label>
      <Input name="name" type="text" onChange={handleChange} value={formData.name} required />
      <label className="block mt-4 mb-2">Email</label>
      <Input name="email" type="email" onChange={handleChange} value={formData.email} required />
      <label className="block mt-4 mb-2">Phone Number</label>
      <Input name="phone" type="tel" onChange={handleChange} value={formData.phone} required />
    </div>
  ], [formData]);

  return (
    <div className="min-h-screen bg-[#f9fafb] flex items-center justify-center p-6">
      <Card className="w-full max-w-xl shadow-2xl border-t-8 border-[#2eb97f]">
        <CardContent className="p-6">
          <h1 className="text-3xl font-bold mb-4 text-center text-[#1a2b4c]">Welcome to WellthMatch</h1>
          <p className="text-center mb-6 text-gray-700">Let’s find the right financial guide for your goals. Get matched in under 2 minutes.</p>
          {submitted ? (
            <div className="text-green-600 text-center text-lg">
              <p>Thanks! You’ve been matched with:</p>
              <p className="font-semibold mt-2">{matchedAdvisor.name}</p>
              <p>{matchedAdvisor.firm}</p>
              <p className="text-sm">Contact: {matchedAdvisor.contact}</p>
            </div>
          ) : (
            <form onSubmit={handleSubmit} className="space-y-4">
              {steps[step - 1]}
              <div className="flex justify-between mt-4">
                {step > 1 && <Button type="button" onClick={handleBack} variant="outline">Back</Button>}
                {step < steps.length ? (
                  <Button type="button" onClick={handleNext}>Next</Button>
                ) : (
                  <Button type="submit">Submit</Button>
                )}
              </div>
            </form>
          )}
        </CardContent>
      </Card>
    </div>
  );
}
