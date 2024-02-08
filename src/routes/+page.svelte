<script lang="ts">
    import { Button, buttonVariants } from "$lib/components/ui/button";
    import * as Card from "$lib/components/ui/card";
    import * as Select from "$lib/components/ui/select";
    import { Input } from "$lib/components/ui/input";
    import { Label } from "$lib/components/ui/label";
    import { Sun, Moon } from "radix-icons-svelte";
    import { toast } from "svelte-sonner";
    import { toggleMode } from "mode-watcher";

    import * as Dialog from "$lib/components/ui/dialog";

    const frameworks = [
        {
            value: "sveltekit",
            label: "SvelteKit",
        },
        {
            value: "next",
            label: "Next.js",
        },
        {
            value: "astro",
            label: "Astro",
        },
        {
            value: "nuxt",
            label: "Nuxt.js",
        },
    ];
</script>

<Button on:click={toggleMode} variant="outline" size="icon">
    <Sun
        class="h-[1.2rem] w-[1.2rem] rotate-0 scale-100 transition-all dark:-rotate-90 dark:scale-0"
    />
    <Moon
        class="absolute h-[1.2rem] w-[1.2rem] rotate-90 scale-0 transition-all dark:rotate-0 dark:scale-100"
    />
    <span class="sr-only">Toggle theme</span>
</Button>

<Card.Root class="w-[350px]">
    <Card.Header>
        <Card.Title>Create project</Card.Title>
        <Card.Description
            >Deploy your new project in one-click.</Card.Description
        >
    </Card.Header>
    <Card.Content>
        <form>
            <div class="grid w-full items-center gap-4">
                <div class="flex flex-col space-y-1.5">
                    <Label for="name">Name</Label>
                    <Input id="name" placeholder="Name of your project" />
                </div>
                <div class="flex flex-col space-y-1.5">
                    <Label for="framework">Framework</Label>
                    <Select.Root>
                        <Select.Trigger id="framework">
                            <Select.Value placeholder="Select" />
                        </Select.Trigger>
                        <Select.Content>
                            {#each frameworks as framework}
                                <Select.Item
                                    value={framework.value}
                                    label={framework.label}
                                    >{framework.label}</Select.Item
                                >
                            {/each}
                        </Select.Content>
                    </Select.Root>
                </div>
            </div>
        </form>
    </Card.Content>
    <Card.Footer class="flex justify-between">
        <Button variant="outline">Cancel</Button>
        <Button>Deploy</Button>
    </Card.Footer>
</Card.Root>

<Button
    variant="outline"
    on:click={() =>
        toast("Event has been created", {
            description: "Sunday, December 03, 2023 at 9:00 AM",
            action: {
                label: "Undo",
                onClick: () => console.log("Undo"),
            },
        })}
>
    Show Toast
</Button>

<Dialog.Root>
    <Dialog.Trigger class={buttonVariants({ variant: "outline" })}
        >Edit Profile</Dialog.Trigger
    >
    <Dialog.Content class="sm:max-w-[425px]">
        <Dialog.Header>
            <Dialog.Title>Edit profile</Dialog.Title>
            <Dialog.Description>
                Make changes to your profile here. Click save when you're done.
            </Dialog.Description>
        </Dialog.Header>
        <div class="grid gap-4 py-4">
            <div class="grid grid-cols-4 items-center gap-4">
                <Label for="name" class="text-right">Name</Label>
                <Input id="name" value="Pedro Duarte" class="col-span-3" />
            </div>
            <div class="grid grid-cols-4 items-center gap-4">
                <Label for="username" class="text-right">Username</Label>
                <Input id="username" value="@peduarte" class="col-span-3" />
            </div>
        </div>
        <Dialog.Footer>
            <Button type="submit">Save changes</Button>
        </Dialog.Footer>
    </Dialog.Content>
</Dialog.Root>