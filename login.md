import 'package:flutter/material.dart';
import 'models/user_model.dart';
import 'services/authentication_service.dart';

class LoginScreen extends StatelessWidget {
  final AuthenticationService authService = AuthenticationService();

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('Login')),
      body: Padding(
        padding: const EdgeInsets.all(16.0),
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            TextField(
              decoration: InputDecoration(labelText: 'Username'),
            ),
            TextField(
              obscureText: true,
              decoration: InputDecoration(labelText: 'Password'),
            ),
            SizedBox(height: 20),
            ElevatedButton(
              onPressed: () async {
                // Fetch username and password from text fields
                final UserModel user = UserModel(
                  username: 'example', // Replace with actual username
                  password: 'password', // Replace with actual password
                );

                final bool isAuthenticated = await authService.login(user);

                if (isAuthenticated) {
                  // Navigate to the dashboard
                  Navigator.pushReplacementNamed(context, '/dashboard');
                } else {
                  // Show authentication error
                  ScaffoldMessenger.of(context).showSnackBar(
                    SnackBar(content: Text('Authentication failed')),
                  );
                }
              },
              child: Text('Login'),
            ),
          ],
        ),
      ),
    );
  }
}
