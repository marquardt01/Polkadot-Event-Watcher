# Polkadot-Event-Watcher
This script allows you to subscribe to specific events on the Polkadot network and receive real-time updates
const { ApiPromise, WsProvider } = require('@polkadot/api');

async function watchEvents() {
  // Connect to the Polkadot network
  const provider = new WsProvider('wss://rpc.polkadot.io');
  const api = await ApiPromise.create({ provider });

  // Subscribe to specific events
  api.query.system.events((events) => {
    events.forEach((record) => {
      const { event } = record;
      console.log(`New Event: ${event.section}.${event.method}`);
      console.log(`Data: ${event.data}`);
      console.log('-------------------------------------------');
    });
  });
}

// Usage example
(async () => {
  await watchEvents();
})();
