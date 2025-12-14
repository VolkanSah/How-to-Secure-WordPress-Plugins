# How to Secure WordPress Plugins (Like a Pro)

### A Hands-On Guide to Preventing SQL Injection

This repository is a practical demonstration that confronts a critical security flaw in WordPress plugin development. It directly compares a dangerously insecure method for handling user input with a robust, professional approach.

-   **Vulnerable:** Directly uses unsanitized user input from `$_GET` in a database query, creating a high-risk SQL injection vulnerability.
-   **Secure:** Employs a PDO-based approach with genuine prepared statements to safely handle public input, ensuring bulletproof security.

---

##  The Core Problem: WordPress Database Handling

Many developers unknowingly create insecure plugins because of a common misconception about the native `$wpdb->prepare()` method.

**This is a crucial distinction:**
The WordPress `$wpdb->prepare()` function is **not** a true prepared statement implementation in the same way that PDO is. It uses a `sprintf`-like string substitution, which, while useful for basic sanitization, does not offer the same level of protection as a genuine prepared statement. Our secure example bypasses this limitation by using a PDO-based connection directly, ensuring that the query structure and user data are completely separated at the database level. This provides a significantly higher level of protection against SQL injection attacks.

---

##  The Dangers Unpacked: Vulnerable vs. Secure

| Insecure (`vulnerable`) | Secure (`secure`) |
| :--- | :--- |
| Direct string concatenation of `$_GET` input. | Uses PDO with proper prepared statements. |
| **Wide open to SQL Injection attacks.** | **Fully protected against SQL Injection.** |
| A quick, simple, but dangerous approach. | A robust, production-ready solution. |
| For demonstration purposes only. 🔥 | The definitive professional approach. ✅ |

---

## 🛠️ Installation & Testing

> [!WARNING]
> The **vulnerable** version is intentionally insecure. **DO NOT INSTALL OR RUN THIS ON PUBLIC SERVERS!** Use a local development environment for testing purposes.

### Installation

1.  Clone this repository to your local machine.
2.  Place both plugin folders (`vulnerable` and `secure`) into your local WordPress installation's `/wp-content/plugins/` directory.
3.  Activate both plugins from the WordPress admin dashboard.

### Shortcode Usage

-   For the **vulnerable** version, insert `[get_user]` into a page or post.
-   For the **secure** version, insert `[get_user_secure]` into a separate page or post.

### Test Scenarios

#### SQL Injection Test

1.  **Vulnerable Plugin:**
    -   Navigate to the page with the `[get_user]` shortcode.
    -   Append the URL with a malicious payload, for example: `?user_id=1 OR 1=1 --`
    -   **Expected Result:** The insecure plugin will likely return data for all users, demonstrating a successful SQL injection.

2.  **Secure Plugin:**
    -   Navigate to the page with the `[get_user_secure]` shortcode.
    -   Append the URL with the same payload: `?user_id=1 OR 1=1 --`
    -   **Expected Result:** The secure plugin will correctly treat `1 OR 1=1 --` as a single, invalid parameter and return "No user found."

---

## 🛡️ Why Security Matters

> **"An insecure plugin is like a gaping hole in your site’s security. A single line of malicious code can compromise your entire database and reputation."**

The goal of this project is to provide a clear, undeniable demonstration of secure coding principles. By implementing true prepared statements, you are not just writing code that works—you are building a fortress that protects your website and, more importantly, your users' data from malicious attacks.

---

##  Additional Resources

-   [OWASP Top 10 – SQL Injection](https://owasp.org/www-project-top-ten/)
-   [WordPress Plugin Developer Handbook – Security](https://developer.wordpress.org/plugins/security/)
-   [PDO Prepared Statements](https://www.php.net/manual/en/pdo.prepared-statements.php)

---

##  Final Note

This project is a call to action for all developers: **If you handle public input, write your code with security in mind.** Your plugins are the guardians of your users' data. Don't let them be the weakest link.

---

## License

MIT License

Copyright (c) 2025 Volkan Kücükbudak

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included
in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.


