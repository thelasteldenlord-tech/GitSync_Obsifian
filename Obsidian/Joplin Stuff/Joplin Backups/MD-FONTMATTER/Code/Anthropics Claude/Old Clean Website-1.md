---
title: 'Old Clean Website '
updated: 2025-09-02 07:42:54Z
created: 2025-09-02 07:42:07Z
---

``` html

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>SparkleClean Pro - Premium Cleaning Services</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            line-height: 1.6;
            color: #333;
            overflow-x: hidden;
        }

        .hero {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            min-height: 100vh;
            display: flex;
            align-items: center;
            position: relative;
            overflow: hidden;
        }

        .hero::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: url('data:image/svg+xml,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 1000 1000"><circle cx="200" cy="200" r="100" fill="rgba(255,255,255,0.1)"/><circle cx="800" cy="300" r="150" fill="rgba(255,255,255,0.05)"/><circle cx="300" cy="700" r="80" fill="rgba(255,255,255,0.08)"/></svg>');
            animation: float 20s ease-in-out infinite;
        }

        @keyframes float {
            0%, 100% { transform: translateY(0px); }
            50% { transform: translateY(-20px); }
        }

        .hero-content {
            max-width: 1200px;
            margin: 0 auto;
            padding: 0 20px;
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 50px;
            align-items: center;
            position: relative;
            z-index: 2;
        }

        .hero-text h1 {
            font-size: 3.5rem;
            font-weight: 700;
            margin-bottom: 20px;
            background: linear-gradient(45deg, #fff, #e0e0ff);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }

        .hero-text p {
            font-size: 1.3rem;
            margin-bottom: 30px;
            opacity: 0.9;
        }

        .cta-button {
            background: linear-gradient(45deg, #ff6b6b, #ee5a24);
            color: white;
            padding: 18px 40px;
            border: none;
            border-radius: 50px;
            font-size: 1.2rem;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 10px 30px rgba(255, 107, 107, 0.3);
        }

        .cta-button:hover {
            transform: translateY(-3px);
            box-shadow: 0 15px 40px rgba(255, 107, 107, 0.4);
        }

        .booking-form {
            background: rgba(255, 255, 255, 0.95);
            backdrop-filter: blur(10px);
            padding: 40px;
            border-radius: 20px;
            box-shadow: 0 20px 60px rgba(0, 0, 0, 0.1);
            color: #333;
        }

        .booking-form h3 {
            color: #667eea;
            margin-bottom: 25px;
            font-size: 1.8rem;
        }

        .form-group {
            margin-bottom: 20px;
        }

        .form-group label {
            display: block;
            margin-bottom: 8px;
            font-weight: 600;
            color: #555;
        }

        .form-group input, .form-group select, .form-group textarea {
            width: 100%;
            padding: 12px 15px;
            border: 2px solid #e0e0e0;
            border-radius: 10px;
            font-size: 1rem;
            transition: border-color 0.3s ease;
        }

        .form-group input:focus, .form-group select:focus, .form-group textarea:focus {
            outline: none;
            border-color: #667eea;
        }

        .services-section {
            padding: 100px 0;
            background: linear-gradient(45deg, #f093fb 0%, #f5576c 100%);
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 0 20px;
        }

        .section-title {
            text-align: center;
            font-size: 3rem;
            color: white;
            margin-bottom: 60px;
            font-weight: 700;
        }

        .services-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 40px;
        }

        .service-card {
            background: white;
            padding: 40px 30px;
            border-radius: 20px;
            text-align: center;
            box-shadow: 0 15px 40px rgba(0, 0, 0, 0.1);
            transition: transform 0.3s ease;
            position: relative;
            overflow: hidden;
        }

        .service-card::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.4), transparent);
            transition: left 0.5s;
        }

        .service-card:hover::before {
            left: 100%;
        }

        .service-card:hover {
            transform: translateY(-10px);
        }

        .service-icon {
            font-size: 4rem;
            margin-bottom: 20px;
        }

        .testimonials {
            padding: 100px 0;
            background: #f8f9fa;
        }

        .testimonial-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
            gap: 40px;
        }

        .testimonial-card {
            background: white;
            padding: 40px;
            border-radius: 20px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
            position: relative;
        }

        .testimonial-card::before {
            content: '"';
            position: absolute;
            top: -10px;
            left: 20px;
            font-size: 6rem;
            color: #667eea;
            opacity: 0.3;
        }

        .contact-section {
            padding: 100px 0;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
        }

        .contact-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 60px;
            align-items: center;
        }

        .footer {
            background: #2c3e50;
            color: white;
            padding: 50px 0 30px;
            text-align: center;
        }

        @media (max-width: 768px) {
            .hero-content {
                grid-template-columns: 1fr;
                text-align: center;
            }
            
            .hero-text h1 {
                font-size: 2.5rem;
            }
            
            .contact-grid {
                grid-template-columns: 1fr;
            }
        }

        .price-tag {
            background: #ff6b6b;
            color: white;
            padding: 10px 20px;
            border-radius: 25px;
            font-weight: bold;
            display: inline-block;
            margin-top: 15px;
        }

        .before-after {
            padding: 100px 0;
            background: #fff;
        }

        .ba-container {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 40px;
        }

        .ba-item {
            position: relative;
            border-radius: 15px;
            overflow: hidden;
            height: 300px;
            background: linear-gradient(45deg, #ddd, #f0f0f0);
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.2rem;
            color: #666;
            cursor: pointer;
            transition: transform 0.3s ease;
        }

        .ba-item:hover {
            transform: scale(1.05);
        }
    </style>
</head>
<body>
    <header class="hero">
        <div class="hero-content">
            <div class="hero-text">
                <h1>Spotless Results, Every Time</h1>
                <p>Professional cleaning services that transform your space into a pristine sanctuary. We don't just clean – we create environments where you thrive.</p>
                <button class="cta-button" onclick="document.querySelector('.booking-form').scrollIntoView({behavior: 'smooth'})">
                    Get Instant Quote
                </button>
            </div>
            
            <div class="booking-form">
                <h3>Book Your Service Now</h3>
                <form id="bookingForm">
                    <div class="form-group">
                        <label for="service">Service Type</label>
                        <select id="service" name="service" required>
                            <option value="">Select a service</option>
                            <option value="regular">Regular Cleaning - $120</option>
                            <option value="deep">Deep Cleaning - $200</option>
                            <option value="move">Move In/Out - $250</option>
                            <option value="office">Office Cleaning - Quote</option>
                        </select>
                    </div>
                    
                    <div class="form-group">
                        <label for="date">Preferred Date</label>
                        <input type="date" id="date" name="date" required>
                    </div>
                    
                    <div class="form-group">
                        <label for="name">Your Name</label>
                        <input type="text" id="name" name="name" required>
                    </div>
                    
                    <div class="form-group">
                        <label for="phone">Phone Number</label>
                        <input type="tel" id="phone" name="phone" required>
                    </div>
                    
                    <div class="form-group">
                        <label for="address">Address</label>
                        <input type="text" id="address" name="address" required>
                    </div>
                    
                    <button type="submit" class="cta-button" style="width: 100%;">
                        Book My Cleaning Service
                    </button>
                </form>
            </div>
        </div>
    </header>

    <section class="services-section">
        <div class="container">
            <h2 class="section-title">Our Premium Services</h2>
            <div class="services-grid">
                <div class="service-card">
                    <div class="service-icon">🏠</div>
                    <h3>Regular Home Cleaning</h3>
                    <p>Weekly, bi-weekly, or monthly cleaning to keep your home consistently spotless. We handle everything from kitchens to bathrooms.</p>
                    <div class="price-tag">Starting at $120</div>
                </div>
                
                <div class="service-card">
                    <div class="service-icon">✨</div>
                    <h3>Deep Cleaning</h3>
                    <p>Comprehensive top-to-bottom cleaning that reaches every corner, perfect for spring cleaning or special occasions.</p>
                    <div class="price-tag">Starting at $200</div>
                </div>
                
                <div class="service-card">
                    <div class="service-icon">📦</div>
                    <h3>Move In/Out Cleaning</h3>
                    <p>Make your transition smooth with our thorough move-in or move-out cleaning service. Leave the cleaning to us!</p>
                    <div class="price-tag">Starting at $250</div>
                </div>
                
                <div class="service-card">
                    <div class="service-icon">🏢</div>
                    <h3>Office Cleaning</h3>
                    <p>Professional commercial cleaning services to maintain a productive and healthy work environment for your team.</p>
                    <div class="price-tag">Custom Quote</div>
                </div>
            </div>
        </div>
    </section>

    <section class="before-after">
        <div class="container">
            <h2 class="section-title" style="color: #333;">See The Difference</h2>
            <div class="ba-container">
                <div class="ba-item">
                    <div>Before: Cluttered Kitchen → After: Sparkling Clean</div>
                </div>
                <div class="ba-item">
                    <div>Before: Dusty Living Room → After: Fresh & Organized</div>
                </div>
                <div class="ba-item">
                    <div>Before: Messy Bathroom → After: Hotel-Quality Clean</div>
                </div>
            </div>
        </div>
    </section>

    <section class="testimonials">
        <div class="container">
            <h2 class="section-title" style="color: #333;">What Our Clients Say</h2>
            <div class="testimonial-grid">
                <div class="testimonial-card">
                    <p>Best cleaning service I've ever used! They pay attention to every detail and my house has never looked better. Worth every penny!</p>
                    <h4>- Sarah M., Homeowner</h4>
                </div>
                
                <div class="testimonial-card">
                    <p>Professional, reliable, and thorough. They've been cleaning our office for 6 months and we couldn't be happier with the results.</p>
                    <h4>- Mike R., Business Owner</h4>
                </div>
                
                <div class="testimonial-card">
                    <p>The deep cleaning service was incredible! They transformed my home and I felt like I was living in a brand new space.</p>
                    <h4>- Jennifer L., Satisfied Customer</h4>
                </div>
            </div>
        </div>
    </section>

    <section class="contact-section">
        <div class="container">
            <div class="contact-grid">
                <div>
                    <h2>Ready to Transform Your Space?</h2>
                    <p style="font-size: 1.2rem; margin: 20px 0;">Don't wait – your spotless space is just one call away. We're here to make your life easier and your environment healthier.</p>
                    <div style="margin: 30px 0;">
                        <h3>📞 Call: (555) 123-CLEAN</h3>
                        <h3>✉️ Email: hello@sparklecleanpro.com</h3>
                        <h3>⏰ Available 7 Days a Week</h3>
                    </div>
                </div>
                <div>
                    <h3>Why Choose Us?</h3>
                    <ul style="list-style: none; padding: 0;">
                        <li style="margin: 15px 0;">✅ Fully Insured & Bonded</li>
                        <li style="margin: 15px 0;">✅ Eco-Friendly Products</li>
                        <li style="margin: 15px 0;">✅ 100% Satisfaction Guarantee</li>
                        <li style="margin: 15px 0;">✅ Flexible Scheduling</li>
                        <li style="margin: 15px 0;">✅ Background-Checked Staff</li>
                    </ul>
                </div>
            </div>
        </div>
    </section>

    <footer class="footer">
        <div class="container">
            <p>&copy; 2025 SparkleClean Pro. All rights reserved. | Licensed & Insured</p>
        </div>
    </footer>

    <script>
        // Form submission handling
        document.getElementById('bookingForm').addEventListener('submit', function(e) {
            e.preventDefault();
            
            const formData = new FormData(this);
            const data = Object.fromEntries(formData);
            
            // Here you would typically send to your server
            // For now, we'll show a success message
            alert('Thank you! We\'ll contact you within 2 hours to confirm your booking.');
            
            // You can integrate with services like:
            // - Formspree.io for form handling
            // - Google Sheets API
            // - Your own backend
            
            console.log('Booking data:', data);
        });

        // Set minimum date to today
        document.getElementById('date').min = new Date().toISOString().split('T')[0];
    </script>
</body>
</html>