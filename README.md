# Azure Budget Static Site

A cost-optimized static website hosting solution on Azure with integrated contact form functionality.

## Architecture

For a detailed overview of the cost-optimized system architecture, including pricing estimates and deployment strategies, see [architecture/overview.md](architecture/overview.md).

The architecture leverages Azure's free tiers and consumption-based pricing to minimize costs while providing scalable static website hosting with dynamic contact form capabilities.

## Project Structure

```
azure-static-website-hosting/
├── .gitignore           # Git ignore file
├── LICENSE              # MIT License
├── README.md            # This file
├── RENAME.md            # Repository rename instructions
├── index.html           # Sample homepage
├── architecture/        # Architecture documentation and diagrams
└── contact-form/
    ├── fcf.form.htm     # Main contact form HTML
    └── assets/
        ├── fcf.config.php # Configuration file for form settings
        ├── fcf.process.php # Form processing script
        ├── process.php    # Main processing logic
        ├── classes/       # PHP classes (PHPMailer, validation, etc.)
        ├── css/           # Form styling
        ├── js/            # Form validation scripts
        ├── email-templates/ # HTML and text email templates
        └── lang/          # Language files
```

## Prerequisites

- Azure subscription
- GitHub account (for CI/CD deployment)
- PHP 7.4+ (for local testing of contact form)
- Web server with PHP support (for production contact form)

## Deployment

### Option 1: Azure Static Web Apps (Recommended for static content)

1. Fork this repository to your GitHub account
2. Create a new Azure Static Web App in the Azure portal
3. Connect your GitHub repository
4. Configure the build settings:
   - Build preset: Custom
   - App location: `/`
   - Output location: `/`
5. Deploy

**Note**: The contact form requires PHP processing. For full functionality, you'll need to host the contact form separately on a PHP-enabled server (see Option 2).

### Option 2: Azure App Service (For full PHP support)

1. Create an Azure App Service with PHP runtime
2. Clone this repository
3. Configure the contact form (see below)
4. Deploy via Git or FTP

## Contact Form Configuration

The contact form uses a free script from FreeContactForm.com. To configure:

1. Edit `contact-form/assets/fcf.config.php`:
   - Set `EMAIL_TO` to your email address
   - Configure SMTP settings if using external mail server
   - Customize validation rules if needed

2. Update email templates in `contact-form/assets/email-templates/`:
   - `fcf.email-in.htm` / `fcf.email-in.txt`: Email sent to you
   - `fcf.email-out.htm` / `fcf.email-out.txt`: Auto-response to sender

3. For SMTP configuration:
   ```php
   define('USE_SMTP', 'YES');
   define('SMTP_HOST', 'your-smtp-server.com');
   define('SMTP_USER', 'your-email@domain.com');
   define('SMTP_PASS', 'your-password');
   define('SMTP_PORT', '587');
   define('SMTP_SECURE', 'STARTTLS');
   ```

## Usage

1. Include the contact form in your static pages:
   ```html
   <iframe src="contact-form/fcf.form.htm" width="100%" height="600px"></iframe>
   ```
   Or copy the form HTML directly into your pages.

2. Ensure the form action points to the correct processing script.

## Local Development

1. Start a local PHP server:
   ```bash
   cd contact-form
   php -S localhost:8000
   ```

2. Open `http://localhost:8000/fcf.form.htm` in your browser

## Cost Optimization

This setup is designed for minimal costs:

- **Free Tier**: Azure Static Web Apps (up to 100GB bandwidth)
- **Pay-per-Use**: App Service consumption plan (~$0.20 per 1M requests)
- **Free Email**: Gmail SMTP or SendGrid free tier
- **Typical Cost**: $0-5/month for personal/business sites

See the [architecture documentation](architecture/overview.md) for detailed cost analysis.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Submit a pull request

## Support

For issues related to the contact form script, visit [FreeContactForm.com](https://www.freecontactform.com).

For Azure deployment issues, check the [Azure documentation](https://docs.microsoft.com/en-us/azure/static-web-apps/).