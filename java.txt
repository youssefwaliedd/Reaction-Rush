//full java code
package testing;

public class ReceiverAPP {

    public static void main(String[] args) {

        SerialPortHandle port = new SerialPortHandle("COM5");

        System.out.println("Receiver Ready. Listening for packets...\n");

        int p1 = 0;
        int p2 = 0;

        while (true) {
            try {
                String line = port.readLine().trim();

                // Ignore empty lines or debug text
               // if (!line.matches("\\d+")) {
                   // continue;   // skip anything that isn't a number
                //}

                // Now it's safe to parse
                int packet = Integer.parseInt(line);

                int playerID = (packet >> 4) & 0x0F;
                int eventCode = packet & 0x0F;

                System.out.println(">> Packet Received: " + packet);
                System.out.println("Player: " + playerID);
                System.out.println("Event : " + eventCode);

                if (playerID == 1) p1++;
                if (playerID == 2) p2++;

                System.out.println("SCORES → P1: " + p1 + "  |  P2: " + p2);
                System.out.println("--------------------------------\n");

            } catch (Exception e) {
                // Should never happen now
                System.out.println("Skipping malformed input...");
            }
        }
    }
}
