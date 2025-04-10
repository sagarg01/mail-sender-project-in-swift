# mail-sender-project-in-swift
//
//  ViewController.swift
//  MailSender
//
// 

import UIKit
import SwiftSMTP

class ViewController: UIViewController {
    
    let smtp = SMTP(
        hostname: "smtp.gmail.com",
        email: "sagarhr8853@gmail.com",
        password: "ogkv jnmg xsfw qdjx",//  gmail app password
        port: 587,
        tlsMode: .requireSTARTTLS,
        authMethods: [.plain, .login]
    )

    let from = Mail.User(name: "Sk", email: "sagarhr8853@gmail.com")
    let subject = "Request for Service of Coll Pad"//   subject of mail 

    let body = """
    Dear Tan90 Thermal Solutions Team,

    I hope this message finds you well. I am writing to request a service for my coll pad, as it has been 11 months since the last service. To ensure that the coll pad remains in optimal condition, I believe it is time for a maintenance check.

    Kindly assist me in scheduling a service at your earliest convenience. You can book a service slot by visiting your website at Tan90Thermal.com.

    Thank you for your prompt attention to this matter. I look forward to hearing from you.

    Best regards,
    """

    let recipientEmails = [
       // "mohitsindwani61@gmail.com",
          "aadilkhan868685@gmail.com",
          "shivam721088@gmail.com",
          "alifansari1999@gmail.com"// reciver mails
]

    override func viewDidLoad() {
        super.viewDidLoad()
        // Do any additional setup after loading the view.
        for email in recipientEmails {
            let to = Mail.User(email: email)
            let mail = Mail(from: from, to: [to], subject: subject, text: body)
            
            smtp.send(mail) { (error) in
                if let error = error {
                    print("Failed to send to \(email): \(error)")
                } else {
                    print("Email successfully sent to \(email)")
                }
            }
        }
        
    }
}
