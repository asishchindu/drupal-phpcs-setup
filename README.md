# Setting Up PHP CodeSniffer (PHPCS) for Drupal

This guide explains how to set up **PHP CodeSniffer (PHPCS)** with **Drupal coding standards** in your Drupal project.

---

## 📌 Prerequisites
Ensure you have the following installed:
- **PHP** (7.4+ recommended)
- **Composer**
- **A Drupal project**

---

## 🚀 Installation Steps

### Step 1: Install PHPCS
You can install PHPCS globally or within your project.

#### Global Installation:
```sh
composer global require "squizlabs/php_codesniffer=*"
```

#### Project-specific Installation:
```sh
composer require --dev squizlabs/php_codesniffer
```

---

### Step 2: Install Drupal Coding Standards
```sh
composer require --dev drupal/coder
```

---

### Step 3: Configure PHPCS to Use Drupal Standards
Set the correct coding standards path:
```sh
vendor/bin/phpcs --config-set installed_paths vendor/drupal/coder/coder_sniffer
```

Verify that Drupal standards are recognized:
```sh
vendor/bin/phpcs -i
```
Expected output:
```
The installed coding standards are ... Drupal, DrupalPractice
```

---

### Step 4: Run PHPCS to Check Code Quality
To analyze your custom module’s code:
```sh
vendor/bin/phpcs --standard=Drupal web/modules/custom
```
For best practices:
```sh
vendor/bin/phpcs --standard=DrupalPractice web/modules/custom
```

---

### Step 5: Fix Code Automatically (Optional)
```sh
vendor/bin/phpcbf --standard=Drupal web/modules/custom
```

---

## 🛠 Troubleshooting

### ❌ Error: "Referenced sniff 'SlevomatCodingStandard.Classes.BackedEnumTypeSpacing' does not exist"
This occurs when PHPCS is missing dependencies.

#### ✅ Solution:
1. Install the missing package:
   ```sh
   composer require --dev slevomat/coding-standard
   ```
2. If the issue persists, clear cache and reinstall:
   ```sh
   composer clear-cache
   composer remove squizlabs/php_codesniffer drupal/coder slevomat/coding-standard
   composer require --dev squizlabs/php_codesniffer drupal/coder slevomat/coding-standard
   ```
3. Reconfigure PHPCS:
   ```sh
   vendor/bin/phpcs --config-set installed_paths vendor/drupal/coder/coder_sniffer
   ```
4. Verify installation:
   ```sh
   vendor/bin/phpcs -i
   ```
5. Run PHPCS again:
   ```sh
   vendor/bin/phpcs --standard=Drupal web/modules/custom
   ```

---

## 🎯 Automate PHPCS in Git Pre-commit Hook (Optional)
To enforce standards before committing code:
```sh
echo 'vendor/bin/phpcs --standard=Drupal web/modules/custom' > .git/hooks/pre-commit
chmod +x .git/hooks/pre-commit
```

---

## 🎉 You're All Set!
Now, PHPCS is configured for your Drupal project, ensuring your code follows **Drupal coding standards**. 🚀

💡 *Tip:* Consider integrating PHPCS with your CI/CD pipeline for automated code quality checks!

---

**🔗 Useful Links:**
- [Drupal Coding Standards](https://www.drupal.org/docs/develop/standards)
- [PHP CodeSniffer](https://github.com/squizlabs/PHP_CodeSniffer)
- [Drupal Coder](https://github.com/Drupal-Coder/coder)

