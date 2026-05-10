import 'package:flutter/material.dart';
import 'package:url_launcher/url_launcher.dart';

void main() {
  runApp(const MyPortfolioApp());
}

class MyPortfolioApp extends StatelessWidget {
  const MyPortfolioApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      theme: ThemeData(useMaterial3: true),
      home: const ProfileScreen(),
    );
  }
}

class ProfileScreen extends StatelessWidget {
  const ProfileScreen({super.key});

  // Helper for launching URLs
  Future<void> _launchURL(String url) async {
    final Uri uri = Uri.parse(url);
    if (!await launchUrl(uri)) throw 'Could not launch $url';
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      backgroundColor: const Color(0xFFFCE4EC), // Soft pink background
      body: Center(
        child: SingleChildScrollView(
          child: Column(
            mainAxisAlignment: MainAxisAlignment.center,
            children: [
              Stack(
                alignment: Alignment.topCenter,
                children: [
                  // 1. The Info Card
                  Container(
                    margin: const EdgeInsets.only(top: 60, left: 20, right: 20),
                    padding: const EdgeInsets.only(top: 70, left: 20, right: 20, bottom: 20),
                    decoration: BoxDecoration(
                      color: Colors.white,
                      borderRadius: BorderRadius.circular(30),
                      boxShadow: [
                        BoxShadow(
                          color: Colors.pink.withValues(alpha:0.1),
                          blurRadius: 20,
                          spreadRadius: 5,
                        )
                      ],
                    ),
                    child: Column(
                      mainAxisSize: MainAxisSize.min,
                      children: [
                        // Name
                        const Text(
                          "AIN AMANI SHAHIRAH BINTI AZIZ",
                          textAlign: TextAlign.center,
                          style: TextStyle(
                            fontSize: 22,
                            fontWeight: FontWeight.bold,
                            letterSpacing: 1.2,
                            color: Colors.pinkAccent,
                          ),
                        ),
                        const SizedBox(height: 8),
                        // DOB / State
                        const Text(
                          "8 March 2004 • Terengganu, Malaysia",
                          style: TextStyle(color: Colors.grey, fontSize: 14),
                        ),
                        const SizedBox(height: 15),
                        const Divider(indent: 40, endIndent: 40),
                        const SizedBox(height: 15),
                        // Bio/Quote
                        const Text(
                          "\"Red Flag, code mix with logic .✨\"",
                          textAlign: TextAlign.center,
                          style: TextStyle(
                            fontStyle: FontStyle.italic,
                            fontSize: 15,
                            color: Colors.black87,
                          ),
                        ),
                        const SizedBox(height: 25),
                        // Contact Buttons
                        Row(
                          mainAxisAlignment: MainAxisAlignment.spaceEvenly,
                          children: [
                            _buildIconButton(Icons.email, () => _launchURL('mailto:amaniain23@gmail.com')),
                            _buildIconButton(Icons.phone, () => _launchURL('tel:+601125172650')),
                            _buildIconButton(Icons.camera_alt, () => _launchURL('https://instagram.com/ymir_fritz001')),
                            _buildIconButton(Icons.code, () => _launchURL('https://github.com/Petra1775')),
                          ],
                        ),
                      ],
                    ),
                  ),
                  // 2. The Profile Picture (Floating)
                  Positioned(
                    top: 0,
                    child: Container(
                      decoration: BoxDecoration(
                        shape: BoxShape.circle,
                        border: Border.all(color: Colors.white, width: 5),
                        boxShadow: [
                          BoxShadow(color: Colors.black.withValues(alpha: 0.1), blurRadius: 10),
                        ],
                      ),
                      child: const CircleAvatar(
                        radius: 60,
                        backgroundColor: Colors.pinkAccent,
                        backgroundImage: AssetImage('assets/profile.jpg'),
                      ),
                    ),
                  ),
                ],
              ),
            ],
          ),
        ),
      ),
    );
  }

  // Quick helper for styled social icons
  Widget _buildIconButton(IconData icon, VoidCallback onPressed) {
    return Container(
      decoration: BoxDecoration(
        color: const Color(0xFFFFF0F5),
        borderRadius: BorderRadius.circular(15),
      ),
      child: IconButton(
        icon: Icon(icon, color: Colors.pinkAccent),
        onPressed: onPressed,
      ),
    );
  }
}
