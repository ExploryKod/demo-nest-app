# Testing JWT Authentication

## Quick Test Script

Run the test script to create a test user and verify authentication:

```bash
cd quizzam
./test-auth.sh
```

This will:
1. Register a test user (or login if already exists)
2. Get a JWT token
3. Test accessing a protected endpoint

## Manual Testing with cURL

### 1. Register a New User

```bash
curl -X POST http://localhost:3000/api/auth/register \
  -H "Content-Type: application/json" \
  -d '{
    "email": "test@example.com",
    "password": "testpassword123",
    "username": "TestUser"
  }'
```

Expected response:
```json
{
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
  "user": {
    "email": "test@example.com",
    "uid": "user_1234567890_abc123",
    "username": "TestUser"
  }
}
```

### 2. Login with Existing User

```bash
curl -X POST http://localhost:3000/api/auth/login \
  -H "Content-Type: application/json" \
  -d '{
    "email": "test@example.com",
    "password": "testpassword123"
  }'
```

### 3. Access Protected Endpoint

```bash
# Replace YOUR_TOKEN with the token from registration/login
curl -X GET http://localhost:3000/api/users/me \
  -H "Authorization: Bearer YOUR_TOKEN"
```

## Testing in Frontend

1. **Start the backend:**
   ```bash
   cd quizzam
   pnpm start
   ```

2. **Start the frontend:**
   ```bash
   cd quizzy-front
   pnpm start
   ```

3. **Open browser:** http://localhost:4200

4. **Register a new user:**
   - Click "Register"
   - Fill in:
     - Email: `test@example.com`
     - Username: `TestUser`
     - Password: `testpassword123`
   - Submit

5. **Or login with existing user:**
   - Click "Login"
   - Use credentials from registration

## Test Credentials

After running the test script, you can use:

- **Email:** `test@example.com`
- **Password:** `testpassword123`
- **Username:** `TestUser`

## Verify Token Storage

Check browser localStorage:
1. Open DevTools (F12)
2. Go to Application/Storage tab
3. Check Local Storage
4. Look for:
   - `jwt_token` - The JWT token
   - `jwt_user` - User information

## Troubleshooting

### Backend not responding
- Check if backend is running: `curl http://localhost:3000/api/ping`
- Check MongoDB connection
- Verify `.env` file has correct `DATABASE_URL`

### Registration fails
- User might already exist - try login instead
- Check MongoDB is running
- Verify password meets requirements (if any)

### Login fails
- Verify user exists in database
- Check password is correct
- Verify JWT_SECRET is set in backend `.env`

### Frontend can't connect
- Verify `environment.development.ts` has correct `apiUrl`
- Check CORS settings in backend
- Verify backend is running on port 3000

