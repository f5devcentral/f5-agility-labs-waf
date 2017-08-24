Results
---------------

#. Open Firefox and navigate to ``https://hackazon.f5demo.com``

#. *(You'll find a toolbar shortcut for the Hackazon link and this can
   be used.)*

   |image8|

#. Interact with the application by clicking the Hackazon logo and any
   of the items under the Special Selection title that appear on the
   front page. **Please** refrain from experimenting with the site using
   any "exploit" techniques that you might be familiar with.

#. On the BIG-IP, navigate to **Security > Event Logs > Application >
   Requests** and verify that requests are being observed.

#. **Tip:** You will need to clear the “Illegal Requests” only filter:

   |image9|

   You should be able to see both the raw client request and server
   response for the event that you selected.

   **For example:**

   |image10|
