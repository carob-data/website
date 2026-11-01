Contact
=======

You can write us with questions and suggestions.

.. raw:: html

   <style>
   .contact-form { max-width: 36rem; }
   .contact-form .form-group { margin-bottom: 1rem; }
   .contact-form label { display: block; margin-bottom: 0.25rem; font-weight: 700; }
   .contact-form .form-control {
     display: block; width: 100%; box-sizing: border-box;
     padding: 0.375rem 0.75rem; font-size: 1rem; line-height: 1.5;
     color: #495057; background: #fff; border: 1px solid #ced4da; border-radius: 0.25rem;
   }
   .contact-form button {
     background-color: #2980b9; color: #fff; border: 0; border-radius: 0.25rem;
     padding: 0.375rem 0.75rem; cursor: pointer;
   }
   .contact-form button:disabled { opacity: 0.65; cursor: default; }
   .contact-form .mt-3 { margin-top: 1rem; }
   </style>
   <form id="contact-form" class="contact-form" action="https://formsubmit.co/ajax/40f42981681c59defba81a32879261e4" method="POST">
     <input type="text" name="_honey" style="display:none" tabindex="-1" autocomplete="off">
     <input type="hidden" name="_subject" value="Carob website message">
     <input type="hidden" name="_template" value="table">
     <div class="form-group">
       <label for="contact-name">Name</label>
       <input class="form-control" id="contact-name" name="name" type="text" required autocomplete="name">
     </div>
     <div class="form-group">
       <label for="contact-email">Email</label>
       <input class="form-control" id="contact-email" name="email" type="email" required autocomplete="email">
     </div>
     <div class="form-group">
       <label for="contact-message">Message</label>
       <textarea class="form-control" id="contact-message" name="message" rows="6" required></textarea>
     </div>
     <button class="btn btn-primary" type="submit">Send</button>
     <p id="contact-status" class="mt-3" role="status"></p>
   </form>
   <script>
     var contactForm = document.getElementById("contact-form");
     var contactStatus = document.getElementById("contact-status");
     contactForm.addEventListener("submit", function (event) {
       event.preventDefault();
       var replyTo = contactForm.querySelector("[name=_replyto]");
       if (!replyTo) {
         replyTo = document.createElement("input");
         replyTo.type = "hidden";
         replyTo.name = "_replyto";
         contactForm.appendChild(replyTo);
       }
       replyTo.value = contactForm.email.value;
       var button = contactForm.querySelector("button");
       button.disabled = true;
       contactStatus.textContent = "Sending…";
       fetch(contactForm.action, {
         method: "POST",
         body: new FormData(contactForm),
         headers: { "Accept": "application/json" }
       }).then(function (response) {
         return response.json().then(function (data) {
           return { ok: response.ok, data: data };
         });
       }).then(function (result) {
         var succeeded = result.ok && String(result.data.success) !== "false";
         if (succeeded) {
           contactForm.reset();
           contactStatus.textContent = "Message sent. Thank you.";
         } else {
           contactStatus.textContent = result.data.message || "The message could not be sent. Please try again.";
         }
       }).catch(function () {
         contactStatus.textContent = "The message could not be sent. Please try again.";
       }).then(function () {
         button.disabled = false;
       });
     });
   </script>
